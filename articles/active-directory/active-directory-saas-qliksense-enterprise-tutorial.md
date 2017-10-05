---
title: "Didacticiel : Intégration d’Azure Active Directory à Qlik Sense Enterprise | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Qlik Sense Enterprise."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8c27e340-2b25-47b6-bf1f-438be4c14f93
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 4964634cd5aaf0dbb98c766f5e12700c4d118750
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qlik-sense-enterprise"></a><span data-ttu-id="5924f-103">Didacticiel : Intégration d’Azure Active Directory à Qlik Sense Enterprise</span><span class="sxs-lookup"><span data-stu-id="5924f-103">Tutorial: Azure Active Directory integration with Qlik Sense Enterprise</span></span>

<span data-ttu-id="5924f-104">Dans ce didacticiel, vous allez apprendre à intégrer Qlik Sense Enterprise à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5924f-104">In this tutorial, you learn how to integrate Qlik Sense Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5924f-105">L’intégration du logiciel Qlik Sense Enterprise à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="5924f-105">Integrating Qlik Sense Enterprise with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5924f-106">Dans Azure AD, vous pouvez contrôler qui a accès à Qlik Sense Enterprise.</span><span class="sxs-lookup"><span data-stu-id="5924f-106">You can control in Azure AD who has access to Qlik Sense Enterprise.</span></span>
- <span data-ttu-id="5924f-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Qlik Sense Enterprise (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5924f-107">You can enable your users to automatically get signed-on to Qlik Sense Enterprise (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="5924f-108">Vous pouvez gérer vos comptes dans un emplacement central : le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5924f-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="5924f-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5924f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5924f-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="5924f-110">Prerequisites</span></span>

<span data-ttu-id="5924f-111">Pour configurer l’intégration d’Azure AD à Qlik Sense Enterprise, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="5924f-111">To configure Azure AD integration with Qlik Sense Enterprise, you need the following items:</span></span>

- <span data-ttu-id="5924f-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="5924f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5924f-113">Un abonnement Qlik Sense Enterprise pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="5924f-113">A Qlik Sense Enterprise single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5924f-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="5924f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5924f-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="5924f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5924f-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="5924f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5924f-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois ici : [offre d’essai](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5924f-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5924f-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="5924f-118">Scenario description</span></span>
<span data-ttu-id="5924f-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="5924f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5924f-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="5924f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5924f-121">Ajout de Qlik Sense Enterprise à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="5924f-121">Adding Qlik Sense Enterprise from the gallery</span></span>
2. <span data-ttu-id="5924f-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5924f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-qlik-sense-enterprise-from-the-gallery"></a><span data-ttu-id="5924f-123">Ajout de Qlik Sense Enterprise à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="5924f-123">Adding Qlik Sense Enterprise from the gallery</span></span>
<span data-ttu-id="5924f-124">Pour configurer l’intégration de Qlik Sense Enterprise à Azure AD, vous devez ajouter Qlik Sense Enterprise depuis la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="5924f-124">To configure the integration of Qlik Sense Enterprise into Azure AD, you need to add Qlik Sense Enterprise from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5924f-125">**Pour ajouter Qlik Sense Enterprise à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5924f-125">**To add Qlik Sense Enterprise from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5924f-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5924f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Bouton Azure Active Directory][1]

2. <span data-ttu-id="5924f-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="5924f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5924f-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5924f-129">Then go to **All applications**.</span></span>

    ![Panneau Applications d’entreprise][2]
    
3. <span data-ttu-id="5924f-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="5924f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Bouton Nouvelle application][3]

4. <span data-ttu-id="5924f-133">Dans la zone de recherche, tapez **Qlik Sense Enterprise**, sélectionnez **Qlik Sense Enterprise** dans le volet de résultats, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="5924f-133">In the search box, type **Qlik Sense Enterprise**, select **Qlik Sense Enterprise** from result panel then click **Add** button to add the application.</span></span>

    ![Qlik Sense Enterprise dans la liste des résultats](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="5924f-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5924f-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="5924f-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Qlik Sense Enterprise avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="5924f-136">In this section, you configure and test Azure AD single sign-on with Qlik Sense Enterprise based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5924f-137">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Qlik Sense Enterprise équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5924f-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Qlik Sense Enterprise is to a user in Azure AD.</span></span> <span data-ttu-id="5924f-138">En d’autres termes, une relation entre un utilisateur Azure AD et l’utilisateur Qlik Sense Enterprise associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="5924f-138">In other words, a link relationship between an Azure AD user and the related user in Qlik Sense Enterprise needs to be established.</span></span>

<span data-ttu-id="5924f-139">Dans Qlik Sense Enterprise, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="5924f-139">In Qlik Sense Enterprise, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5924f-140">Pour configurer et tester l’authentification unique Azure AD avec Qlik Sense Enterprise, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="5924f-140">To configure and test Azure AD single sign-on with Qlik Sense Enterprise, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5924f-141">**[Configurer l’authentification unique Azure AD](#configure-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="5924f-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5924f-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5924f-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5924f-143">**[Créer un utilisateur de test Qlik Sense Enterprise](#create-a-qlik-sense-enterprise-test-user)** pour avoir un équivalent de Britta Simon dans Qlik Sense Enterprise, lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="5924f-143">**[Create a Qlik Sense Enterprise test user](#create-a-qlik-sense-enterprise-test-user)** - to have a counterpart of Britta Simon in Qlik Sense Enterprise that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5924f-144">**[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5924f-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5924f-145">**[Tester l’authentification unique](#test-single-sign-on)** : pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="5924f-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="5924f-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5924f-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="5924f-147">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Qlik Sense Enterprise.</span><span class="sxs-lookup"><span data-stu-id="5924f-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Qlik Sense Enterprise application.</span></span>

<span data-ttu-id="5924f-148">**Pour configurer l’authentification unique Azure AD avec Qlik Sense Enterprise, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5924f-148">**To configure Azure AD single sign-on with Qlik Sense Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="5924f-149">Dans le portail Azure, sur la page d’intégration de l’application **Qlik Sense Enterprise**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="5924f-149">In the Azure portal, on the **Qlik Sense Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="5924f-151">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="5924f-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_samlbase.png)

3. <span data-ttu-id="5924f-153">Dans la section **Domaine et URL Qlik Sense Enterprise**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="5924f-153">On the **Qlik Sense Enterprise Domain and URLs** section, perform the following steps:</span></span>

    ![Informations d’authentification unique de domaine et d’URL Qlik Sense Enterprise](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_url.png)

    <span data-ttu-id="5924f-155">a.</span><span class="sxs-lookup"><span data-stu-id="5924f-155">a.</span></span> <span data-ttu-id="5924f-156">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<Qlik Sense Fully Qualifed Hostname>:443//samlauthn/`</span><span class="sxs-lookup"><span data-stu-id="5924f-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<Qlik Sense Fully Qualifed Hostname>:443//samlauthn/`</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="5924f-157">Notez la barre oblique à la fin de cet URI.</span><span class="sxs-lookup"><span data-stu-id="5924f-157">Note the trailing slash at the end of this URI.</span></span> <span data-ttu-id="5924f-158">Elle est obligatoire.</span><span class="sxs-lookup"><span data-stu-id="5924f-158">It is required.</span></span>
    
    <span data-ttu-id="5924f-159">b.</span><span class="sxs-lookup"><span data-stu-id="5924f-159">b.</span></span> <span data-ttu-id="5924f-160">Dans la zone de texte **Identificateur**, entrez une URL au format suivant :</span><span class="sxs-lookup"><span data-stu-id="5924f-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qlikpoc.com`|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qliksense.com`|

    > [!NOTE] 
    > <span data-ttu-id="5924f-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="5924f-161">These values are not real.</span></span> <span data-ttu-id="5924f-162">Mettez à jour ces valeurs avec l’URL d’authentification et l’identificateur réels qui sont décrits plus loin dans le didacticiel, ou contactez l’[équipe de support technique Qlik Sense Enterprise](https://www.qlik.com/us/services/support) pour obtenir ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="5924f-162">Update these values with the actual Sign-On URL and Identifier, Which are explained later in this tutorial or contact [Qlik Sense Enterprise Client support team](https://www.qlik.com/us/services/support) to get these values.</span></span> 

4. <span data-ttu-id="5924f-163">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="5924f-163">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Lien Téléchargement de certificat](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_certificate.png) 

5. <span data-ttu-id="5924f-165">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="5924f-165">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5924f-167">Préparez le fichier XML de métadonnées de fédération afin de le charger vers le serveur Qlik Sense.</span><span class="sxs-lookup"><span data-stu-id="5924f-167">Prepare the Federation Metadata XML file so that you can upload that to Qlik Sense server.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="5924f-168">Avant de charger les métadonnées IdP vers le serveur Qlik Sense, vous devez modifier le fichier et supprimer des informations pour vous assurer du bon fonctionnement entre Azure AD et le serveur Qlik Sense.</span><span class="sxs-lookup"><span data-stu-id="5924f-168">Before uploading the IdP metadata to the Qlik Sense server, the file needs to be edited to remove information to ensure proper operation between Azure AD and Qlik Sense server.</span></span>
    
    ![QlikSense][qs24]
   
    <span data-ttu-id="5924f-170">a.</span><span class="sxs-lookup"><span data-stu-id="5924f-170">a.</span></span> <span data-ttu-id="5924f-171">Ouvrez le fichier FederationMetaData.xml téléchargé à partir du portail Azure dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="5924f-171">Open the FederationMetaData.xml file, which you have downloaded from Azure portal in a text editor.</span></span>
   
    <span data-ttu-id="5924f-172">b.</span><span class="sxs-lookup"><span data-stu-id="5924f-172">b.</span></span> <span data-ttu-id="5924f-173">Recherchez la valeur **RoleDescriptor**.</span><span class="sxs-lookup"><span data-stu-id="5924f-173">Search for the value **RoleDescriptor**.</span></span>  <span data-ttu-id="5924f-174">Il en existe quatre entrées (deux paires de balises d’élément d’ouverture et de fermeture).</span><span class="sxs-lookup"><span data-stu-id="5924f-174">There are four entries (two pairs of opening and closing element tags).</span></span>
   
    <span data-ttu-id="5924f-175">c.</span><span class="sxs-lookup"><span data-stu-id="5924f-175">c.</span></span> <span data-ttu-id="5924f-176">Dans le fichier, supprimez les balises RoleDescriptor et toutes les informations insérées entre celles-ci.</span><span class="sxs-lookup"><span data-stu-id="5924f-176">Delete the RoleDescriptor tags and all information in between from the file.</span></span>
   
    <span data-ttu-id="5924f-177">d.</span><span class="sxs-lookup"><span data-stu-id="5924f-177">d.</span></span> <span data-ttu-id="5924f-178">Enregistrez le fichier et conservez-le pour l’utiliser ultérieurement dans ce document.</span><span class="sxs-lookup"><span data-stu-id="5924f-178">Save the file and keep it nearby for use later in this document.</span></span>

7. <span data-ttu-id="5924f-179">Accédez à la console de gestion Qlik (QCM) de Qlik Sense en tant qu’utilisateur pouvant créer des configurations de proxy virtuel.</span><span class="sxs-lookup"><span data-stu-id="5924f-179">Navigate to the Qlik Sense Qlik Management Console (QMC) as a user who can create virtual proxy configurations.</span></span>

8. <span data-ttu-id="5924f-180">Dans la console QMC, cliquez sur l’élément de menu **Proxys virtuels**.</span><span class="sxs-lookup"><span data-stu-id="5924f-180">In the QMC, click on the **Virtual Proxies** menu item.</span></span>
   
    ![QlikSense][qs6] 

9. <span data-ttu-id="5924f-182">En bas de l’écran, cliquez sur le bouton **Créer nouveau**.</span><span class="sxs-lookup"><span data-stu-id="5924f-182">At the bottom of the screen, click the **Create new** button.</span></span>
   
    ![QlikSense][qs7]

10. <span data-ttu-id="5924f-184">L’écran Virtual proxy edit (Modification du proxy virtuel) s’affiche.</span><span class="sxs-lookup"><span data-stu-id="5924f-184">The Virtual proxy edit screen appears.</span></span>  <span data-ttu-id="5924f-185">Un menu permettant de rendre les options de configuration visibles est affiché sur le côté droit de l’écran.</span><span class="sxs-lookup"><span data-stu-id="5924f-185">On the right side of the screen is a menu for making configuration options visible.</span></span>
   
    ![QlikSense][qs9]

11. <span data-ttu-id="5924f-187">L’option de menu Identification étant sélectionnée, entrez les informations d’identification pour la configuration du proxy virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="5924f-187">With the Identification menu option checked, enter the identifying information for the Azure virtual proxy configuration.</span></span>
    
    ![QlikSense][qs8]  
    
    <span data-ttu-id="5924f-189">a.</span><span class="sxs-lookup"><span data-stu-id="5924f-189">a.</span></span> <span data-ttu-id="5924f-190">Le champ **Description** contient un nom convivial pour la configuration du proxy virtuel.</span><span class="sxs-lookup"><span data-stu-id="5924f-190">The **Description** field is a friendly name for the virtual proxy configuration.</span></span>  <span data-ttu-id="5924f-191">Entrez une valeur pour la description.</span><span class="sxs-lookup"><span data-stu-id="5924f-191">Enter a value for a description.</span></span>
    
    <span data-ttu-id="5924f-192">b.</span><span class="sxs-lookup"><span data-stu-id="5924f-192">b.</span></span> <span data-ttu-id="5924f-193">Le champ **Préfixe** identifie le point de terminaison proxy virtuel pour la connexion à Qlik Sense avec l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5924f-193">The **Prefix** field identifies the virtual proxy endpoint for connecting to Qlik Sense with Azure AD Single Sign-On.</span></span>  <span data-ttu-id="5924f-194">Entrez un nom de préfixe unique pour ce proxy virtuel.</span><span class="sxs-lookup"><span data-stu-id="5924f-194">Enter a unique prefix name for this virtual proxy.</span></span>
    
    <span data-ttu-id="5924f-195">c.</span><span class="sxs-lookup"><span data-stu-id="5924f-195">c.</span></span> <span data-ttu-id="5924f-196">La valeur **Session inactivity timeout** (Délai d’inactivité de session) (minutes) représente le délai d’expiration des connexions via ce proxy virtuel.</span><span class="sxs-lookup"><span data-stu-id="5924f-196">**Session inactivity timeout (minutes)** is the timeout for connections through this virtual proxy.</span></span>
    
    <span data-ttu-id="5924f-197">d.</span><span class="sxs-lookup"><span data-stu-id="5924f-197">d.</span></span> <span data-ttu-id="5924f-198">La zone **Session cookie header name** (Nom d’en-tête de cookie de session) est le nom du cookie stockant l’identificateur de session pour la session Qlik Sense qu’un utilisateur reçoit après une authentification réussie.</span><span class="sxs-lookup"><span data-stu-id="5924f-198">The **Session cookie header name** is the cookie name storing the session identifier for the Qlik Sense session a user receives after successful authentication.</span></span>  <span data-ttu-id="5924f-199">Ce nom doit être unique.</span><span class="sxs-lookup"><span data-stu-id="5924f-199">This name must be unique.</span></span>

12. <span data-ttu-id="5924f-200">Cliquez sur l’option de menu Authentification pour la rendre visible.</span><span class="sxs-lookup"><span data-stu-id="5924f-200">Click on the Authentication menu option to make it visible.</span></span>  <span data-ttu-id="5924f-201">L’écran Authentification s’affiche.</span><span class="sxs-lookup"><span data-stu-id="5924f-201">The Authentication screen appears.</span></span>
    
    ![QlikSense][qs10]
    
    <span data-ttu-id="5924f-203">a.</span><span class="sxs-lookup"><span data-stu-id="5924f-203">a.</span></span> <span data-ttu-id="5924f-204">La liste déroulante **Anonymous access mode (Mode d’accès anonyme)** détermine si des utilisateurs anonymes peuvent accéder à Qlik Sense via le proxy virtuel.</span><span class="sxs-lookup"><span data-stu-id="5924f-204">The **Anonymous access mode** drop down determines if anonymous users may access Qlik Sense through the virtual proxy.</span></span>  <span data-ttu-id="5924f-205">L’option par défaut est No anonymous user (Pas d’utilisateur anonyme).</span><span class="sxs-lookup"><span data-stu-id="5924f-205">The default option is No anonymous user.</span></span>
    
    <span data-ttu-id="5924f-206">b.</span><span class="sxs-lookup"><span data-stu-id="5924f-206">b.</span></span> <span data-ttu-id="5924f-207">La liste déroulante **Méthode d’authentification** détermine le schéma d’authentification qui sera utilisé par le proxy virtuel.</span><span class="sxs-lookup"><span data-stu-id="5924f-207">The **Authentication method** drop-down determines the authentication scheme the virtual proxy will use.</span></span>  <span data-ttu-id="5924f-208">Dans la liste déroulante, sélectionnez SAML.</span><span class="sxs-lookup"><span data-stu-id="5924f-208">Select SAML from the drop-down list.</span></span>  <span data-ttu-id="5924f-209">À la suite de cette sélection, d’autres options s’affichent.</span><span class="sxs-lookup"><span data-stu-id="5924f-209">More options appear as a result.</span></span>
    
    <span data-ttu-id="5924f-210">c.</span><span class="sxs-lookup"><span data-stu-id="5924f-210">c.</span></span> <span data-ttu-id="5924f-211">Dans le champ **SAML host URI**(URI d’hôte SAML), indiquez le nom d’hôte que les utilisateurs doivent entrer pour accéder à Qlik Sense via ce proxy virtuel SAML.</span><span class="sxs-lookup"><span data-stu-id="5924f-211">In the **SAML host URI field**, input the hostname users enter to access Qlik Sense through this SAML virtual proxy.</span></span>  <span data-ttu-id="5924f-212">Le nom d’hôte est l’URI du serveur Qlik Sense.</span><span class="sxs-lookup"><span data-stu-id="5924f-212">The hostname is the uri of the Qlik Sense server.</span></span>
    
    <span data-ttu-id="5924f-213">d.</span><span class="sxs-lookup"><span data-stu-id="5924f-213">d.</span></span> <span data-ttu-id="5924f-214">Dans le champ **SAML entity ID (ID d’entité SAML)**, entrez la valeur indiquée dans le champ SAML host URI (URI d’hôte SAML).</span><span class="sxs-lookup"><span data-stu-id="5924f-214">In the **SAML entity ID**, enter the same value entered for the SAML host URI field.</span></span>
    
    <span data-ttu-id="5924f-215">e.</span><span class="sxs-lookup"><span data-stu-id="5924f-215">e.</span></span> <span data-ttu-id="5924f-216">La zone **SAML IdP metadata** (Métadonnées IdP SAML) indique le fichier modifié précédemment dans la section **Modifier les métadonnées de fédération dans la configuration d’Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="5924f-216">The **SAML IdP metadata** is the file edited earlier in the **Edit Federation Metadata from Azure AD Configuration** section.</span></span>  <span data-ttu-id="5924f-217">**Avant de charger les métadonnées IdP, vous devez modifier le fichier** et supprimer des informations pour vous assurer du bon fonctionnement entre Azure AD et le serveur Qlik Sense.</span><span class="sxs-lookup"><span data-stu-id="5924f-217">**Before uploading the IdP metadata, the file needs to be edited** to remove information to ensure proper operation between Azure AD and Qlik Sense server.</span></span>  <span data-ttu-id="5924f-218">**Reportez-vous aux instructions ci-dessus si le fichier doit encore être modifié.**</span><span class="sxs-lookup"><span data-stu-id="5924f-218">**Please refer to the instructions above if the file has yet to be edited.**</span></span>  <span data-ttu-id="5924f-219">Si le fichier a été modifié, cliquez sur le bouton Parcourir et sélectionnez le fichier de métadonnées modifié pour le charger vers la configuration du proxy virtuel.</span><span class="sxs-lookup"><span data-stu-id="5924f-219">If the file has been edited click on the Browse button and select the edited metadata file to upload it to the virtual proxy configuration.</span></span>
    
    <span data-ttu-id="5924f-220">f.</span><span class="sxs-lookup"><span data-stu-id="5924f-220">f.</span></span> <span data-ttu-id="5924f-221">Entrez le nom d’attribut ou la référence de schéma pour l’attribut SAML représentant **l’ID utilisateur** qu’Azure AD envoie au serveur Qlik Sense.</span><span class="sxs-lookup"><span data-stu-id="5924f-221">Enter the attribute name or schema reference for the SAML attribute representing the **UserID** Azure AD sends to the Qlik Sense server.</span></span>  <span data-ttu-id="5924f-222">Les informations de référence de schéma sont disponibles dans les écrans de l’application Azure post-configuration.</span><span class="sxs-lookup"><span data-stu-id="5924f-222">Schema reference information is available in the Azure app screens post configuration.</span></span>  <span data-ttu-id="5924f-223">Pour utiliser le nom d’attribut, tapez `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="5924f-223">To use the name attribute, enter `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
    
    <span data-ttu-id="5924f-224">g.</span><span class="sxs-lookup"><span data-stu-id="5924f-224">g.</span></span> <span data-ttu-id="5924f-225">Entrez la valeur du **répertoire utilisateur** qui est attaché aux utilisateurs lorsqu’ils s’authentifient sur le serveur Qlik Sense via Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5924f-225">Enter the value for the **user directory** that will be attached to users when they authenticate to Qlik Sense server through Azure AD.</span></span>  <span data-ttu-id="5924f-226">Les valeurs codées en dur doivent être entourées de **crochets []**.</span><span class="sxs-lookup"><span data-stu-id="5924f-226">Hardcoded values must be surrounded by **square brackets []**.</span></span>  <span data-ttu-id="5924f-227">Pour utiliser un attribut envoyé dans l’assertion SAML Azure AD, entrez son nom dans cette zone de texte **sans** crochets.</span><span class="sxs-lookup"><span data-stu-id="5924f-227">To use an attribute sent in the Azure AD SAML assertion, enter the name of the attribute in this text box **without** square brackets.</span></span>
    
    <span data-ttu-id="5924f-228">h.</span><span class="sxs-lookup"><span data-stu-id="5924f-228">h.</span></span> <span data-ttu-id="5924f-229">**L’algorithme de signature SAML** définit la signature du certificat du fournisseur de service (dans ce cas le serveur Qlik Sense) pour la configuration du proxy virtuel.</span><span class="sxs-lookup"><span data-stu-id="5924f-229">The **SAML signing algorithm** sets the service provider (in this case Qlik Sense server) certificate signing for the virtual proxy configuration.</span></span>  <span data-ttu-id="5924f-230">Si le serveur Qlik Sense utilise un certificat approuvé généré à l’aide de Microsoft Enhanced RSA and AES Cryptographic Provider, définissez l’algorithme de signature SAML sur **SHA-256**.</span><span class="sxs-lookup"><span data-stu-id="5924f-230">If Qlik Sense server uses a trusted certificate generated using Microsoft Enhanced RSA and AES Cryptographic Provider, change the SAML signing algorithm to **SHA-256**.</span></span>
    
    <span data-ttu-id="5924f-231">i.</span><span class="sxs-lookup"><span data-stu-id="5924f-231">i.</span></span> <span data-ttu-id="5924f-232">La section SAML attribute mapping (Mappage d’attributs SAML) permet d’envoyer des attributs supplémentaires, comme des groupes, vers Qlik Sense pour les utiliser dans les règles de sécurité.</span><span class="sxs-lookup"><span data-stu-id="5924f-232">The SAML attribute mapping section allows for additional attributes like groups to be sent to Qlik Sense for use in security rules.</span></span>

13. <span data-ttu-id="5924f-233">Cliquez sur l’option de menu **ÉQUILIBRAGE DE CHARGE** pour la rendre visible.</span><span class="sxs-lookup"><span data-stu-id="5924f-233">Click on the **LOAD BALANCING** menu option to make it visible.</span></span>  <span data-ttu-id="5924f-234">L’écran Équilibrage de charge s’affiche.</span><span class="sxs-lookup"><span data-stu-id="5924f-234">The Load Balancing screen appears.</span></span>
    
    ![QlikSense][qs11]

14. <span data-ttu-id="5924f-236">Cliquez sur le bouton **Add new server node** (Ajouter un nouveau nœud serveur), sélectionnez un ou plusieurs nœuds de moteur auxquels Qlik Sense enverra des sessions à des fins d’équilibrage de charge, puis cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="5924f-236">Click on the **Add new server node** button, select engine node or nodes Qlik Sense will send sessions to for load balancing purposes, and click the **Add** button.</span></span>
    
    ![QlikSense][qs12]

15. <span data-ttu-id="5924f-238">Cliquez sur l’option de menu Avancé pour la rendre visible.</span><span class="sxs-lookup"><span data-stu-id="5924f-238">Click on the Advanced menu option to make it visible.</span></span> <span data-ttu-id="5924f-239">L’écran Avancé s’affiche.</span><span class="sxs-lookup"><span data-stu-id="5924f-239">The Advanced screen appears.</span></span>
    
    ![QlikSense][qs13]
    
    <span data-ttu-id="5924f-241">La liste des hôtes approuvés identifie les noms d’hôte qui sont acceptés lors de la connexion au serveur Qlik Sense.</span><span class="sxs-lookup"><span data-stu-id="5924f-241">The Host white list identifies hostnames that are accepted when connecting to the Qlik Sense server.</span></span>  <span data-ttu-id="5924f-242">**Entrez le nom d’hôte spécifié par les utilisateurs pour se connecter au serveur Qlik Sense.**</span><span class="sxs-lookup"><span data-stu-id="5924f-242">**Enter the hostname users will specify when connecting to Qlik Sense server.**</span></span> <span data-ttu-id="5924f-243">Le nom d’hôte est défini sur la même valeur que l’URI d’hôte SAML sans https://.</span><span class="sxs-lookup"><span data-stu-id="5924f-243">The hostname is the same value as the SAML host uri without the https://.</span></span>

16. <span data-ttu-id="5924f-244">Cliquez sur le bouton **Appliquer**.</span><span class="sxs-lookup"><span data-stu-id="5924f-244">Click the **Apply** button.</span></span>
    
    ![QlikSense][qs14]

17. <span data-ttu-id="5924f-246">Cliquez sur OK pour accepter le message d’avertissement indiquant que les proxys liés au proxy virtuel vont être redémarrés.</span><span class="sxs-lookup"><span data-stu-id="5924f-246">Click OK to accept the warning message that states proxies linked to the virtual proxy will be restarted.</span></span>
    
    ![QlikSense][qs15]

18. <span data-ttu-id="5924f-248">Sur le côté droit de l’écran, le menu Éléments associés s’affiche.</span><span class="sxs-lookup"><span data-stu-id="5924f-248">On the right side of the screen, the Associated items menu appears.</span></span>  <span data-ttu-id="5924f-249">Cliquez sur l’option de menu **Proxys**.</span><span class="sxs-lookup"><span data-stu-id="5924f-249">Click on the **Proxies** menu option.</span></span>
    
    ![QlikSense][qs16]

19. <span data-ttu-id="5924f-251">L’écran Proxy s’affiche.</span><span class="sxs-lookup"><span data-stu-id="5924f-251">The proxy screen appears.</span></span>  <span data-ttu-id="5924f-252">Cliquez sur le bouton **Lier** en bas de l’écran pour lier un proxy au proxy virtuel.</span><span class="sxs-lookup"><span data-stu-id="5924f-252">Click the **Link** button at the bottom to link a proxy to the virtual proxy.</span></span>
    
    ![QlikSense][qs17]

20. <span data-ttu-id="5924f-254">Sélectionnez le nœud proxy qui prendra en charge cette connexion de proxy virtuel et cliquez sur le bouton **Lier**.</span><span class="sxs-lookup"><span data-stu-id="5924f-254">Select the proxy node that will support this virtual proxy connection and click the **Link** button.</span></span>  <span data-ttu-id="5924f-255">Après l’établissement du lien, le proxy est répertorié dans les proxys associés.</span><span class="sxs-lookup"><span data-stu-id="5924f-255">After linking, the proxy will be listed under associated proxies.</span></span>
    
    ![QlikSense][qs18]
  
    ![QlikSense][qs19]

21. <span data-ttu-id="5924f-258">Après environ cinq à dix secondes, le message Refresh QMC (Actualiser la console QMC) s’affiche.</span><span class="sxs-lookup"><span data-stu-id="5924f-258">After about five to ten seconds, the Refresh QMC message will appear.</span></span>  <span data-ttu-id="5924f-259">Cliquez sur le bouton **Refresh QMC** (Actualiser la console QMC).</span><span class="sxs-lookup"><span data-stu-id="5924f-259">Click the **Refresh QMC** button.</span></span>
    
    ![QlikSense][qs20]

22. <span data-ttu-id="5924f-261">Lors de l’actualisation de la console QMC, cliquez sur l’élément de menu **Proxys virtuels**.</span><span class="sxs-lookup"><span data-stu-id="5924f-261">When the QMC refreshes, click on the **Virtual proxies** menu item.</span></span> <span data-ttu-id="5924f-262">La nouvelle entrée de proxy virtuel SAML est indiquée dans le tableau affiché à l’écran.</span><span class="sxs-lookup"><span data-stu-id="5924f-262">The new SAML virtual proxy entry is listed in the table on the screen.</span></span>  <span data-ttu-id="5924f-263">Cliquez sur l’entrée de proxy virtuel.</span><span class="sxs-lookup"><span data-stu-id="5924f-263">Single click on the virtual proxy entry.</span></span>
    
    ![QlikSense][qs51]

23. <span data-ttu-id="5924f-265">En bas de l’écran, le bouton Download SP metadata (Télécharger les métadonnées du fournisseur de service) est activé.</span><span class="sxs-lookup"><span data-stu-id="5924f-265">At the bottom of the screen, the Download SP metadata button will activate.</span></span>  <span data-ttu-id="5924f-266">Cliquez sur le bouton **Download SP metadata** (Télécharger les métadonnées du fournisseur de service) pour enregistrer les métadonnées dans un fichier.</span><span class="sxs-lookup"><span data-stu-id="5924f-266">Click the **Download SP metadata** button to save the metadata to a file.</span></span>
    
    ![QlikSense][qs52]

24. <span data-ttu-id="5924f-268">Ouvrez le fichier de métadonnées du fournisseur de service.</span><span class="sxs-lookup"><span data-stu-id="5924f-268">Open the sp metadata file.</span></span>  <span data-ttu-id="5924f-269">Observez les entrées **entityID** et **AssertionConsumerService**.</span><span class="sxs-lookup"><span data-stu-id="5924f-269">Observe the **entityID** entry and the **AssertionConsumerService** entry.</span></span>  <span data-ttu-id="5924f-270">Ces valeurs sont équivalentes à celles des champs **Identificateur** et **URL de connexion** dans la configuration de l’application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5924f-270">These values are equivalent to the **Identifier** and the **Sign on URL** in the Azure AD application configuration.</span></span> <span data-ttu-id="5924f-271">Collez ces valeurs dans la section **Domaine et URL Qlik Sense Enterprise** de la configuration de l’application Azure AD si elles ne sont pas identiques. Vous devez ensuite les remplacer dans l’assistant de configuration de l’application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5924f-271">Paste these values in the **Qlik Sense Enterprise Domain and URLs** section in the Azure AD application configuration if they are not matching, then you should replace them in the Azure AD App configuration wizard.</span></span>
    
    ![QlikSense][qs53]

> [!TIP]
> <span data-ttu-id="5924f-273">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="5924f-273">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5924f-274">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="5924f-274">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5924f-275">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5924f-275">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="5924f-276">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="5924f-276">Create an Azure AD test user</span></span>
<span data-ttu-id="5924f-277">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5924f-277">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="5924f-279">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5924f-279">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5924f-280">Dans le volet gauche du Portail Azure, cliquez sur le bouton **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5924f-280">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

   ![Bouton Azure Active Directory](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="5924f-282">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="5924f-282">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

   ![Liens « Utilisateurs et groupes » et « Tous les utilisateurs »](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="5924f-284">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="5924f-284">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

   ![Bouton Ajouter](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="5924f-286">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="5924f-286">In the **User** dialog box, perform the following steps:</span></span>

   ![Boîte de dialogue Utilisateur](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_04.png)

   <span data-ttu-id="5924f-288">a.</span><span class="sxs-lookup"><span data-stu-id="5924f-288">a.</span></span> <span data-ttu-id="5924f-289">Dans la zone **Nom**, tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5924f-289">In the **Name** box, type **BrittaSimon**.</span></span>

   <span data-ttu-id="5924f-290">b.</span><span class="sxs-lookup"><span data-stu-id="5924f-290">b.</span></span> <span data-ttu-id="5924f-291">Dans la zone **Nom d’utilisateur** , tapez l’adresse e-mail de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5924f-291">In the **User name** box, type the email address of user Britta Simon.</span></span>

   <span data-ttu-id="5924f-292">c.</span><span class="sxs-lookup"><span data-stu-id="5924f-292">c.</span></span> <span data-ttu-id="5924f-293">Cochez la case **Afficher le mot de passe**, puis notez la valeur affichée dans le champ **Mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="5924f-293">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

   <span data-ttu-id="5924f-294">d.</span><span class="sxs-lookup"><span data-stu-id="5924f-294">d.</span></span> <span data-ttu-id="5924f-295">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="5924f-295">Click **Create**.</span></span>
 
### <a name="create-a-qlik-sense-enterprise-test-user"></a><span data-ttu-id="5924f-296">Créer un utilisateur de test Qlik Sense Enterprise</span><span class="sxs-lookup"><span data-stu-id="5924f-296">Create a Qlik Sense Enterprise test user</span></span>

<span data-ttu-id="5924f-297">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Qlik Sense Enterprise.</span><span class="sxs-lookup"><span data-stu-id="5924f-297">In this section, you create a user called Britta Simon in Qlik Sense Enterprise.</span></span> <span data-ttu-id="5924f-298">Collaborez avec l’[équipe du support technique Qlik Sense Enterprise](https://www.qlik.com/us/services/support) pour ajouter les utilisateurs à la plateforme Qlik Sense Enterprise.</span><span class="sxs-lookup"><span data-stu-id="5924f-298">Work with [Qlik Sense Enterprise Client support team](https://www.qlik.com/us/services/support) to add the users in the Qlik Sense Enterprise platform.</span></span> <span data-ttu-id="5924f-299">Les utilisateurs doivent être créés et activés avant que vous utilisiez l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="5924f-299">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="5924f-300">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="5924f-300">Assign the Azure AD test user</span></span>

<span data-ttu-id="5924f-301">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Qlik Sense Enterprise.</span><span class="sxs-lookup"><span data-stu-id="5924f-301">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Qlik Sense Enterprise.</span></span>

![Attribuer le rôle d’utilisateur][200] 

<span data-ttu-id="5924f-303">**Pour affecter Britta Simon à Qlik Sense Enterprise, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5924f-303">**To assign Britta Simon to Qlik Sense Enterprise, perform the following steps:**</span></span>

1. <span data-ttu-id="5924f-304">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5924f-304">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="5924f-306">Dans la liste des applications, sélectionnez **Qlik Sense Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="5924f-306">In the applications list, select **Qlik Sense Enterprise**.</span></span>

    ![Dans la liste des applications, sélectionnez Qlik Sense Enterprise.](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_app.png)  

3. <span data-ttu-id="5924f-308">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="5924f-308">In the menu on the left, click **Users and groups**.</span></span>

    ![Lien « Utilisateurs et groupes »][202]

4. <span data-ttu-id="5924f-310">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="5924f-310">Click **Add** button.</span></span> <span data-ttu-id="5924f-311">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="5924f-311">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Volet Ajouter une attribution][203]

5. <span data-ttu-id="5924f-313">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="5924f-313">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5924f-314">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="5924f-314">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5924f-315">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="5924f-315">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="5924f-316">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="5924f-316">Test single sign-on</span></span>

<span data-ttu-id="5924f-317">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="5924f-317">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5924f-318">Lorsque vous cliquez sur la mosaïque Qlik Sense Enterprise dans le volet d’accès, vous devez être connecté automatiquement à votre application Qlik Sense Enterprise.</span><span class="sxs-lookup"><span data-stu-id="5924f-318">When you click the Qlik Sense Enterprise tile in the Access Panel, you should get automatically signed-on to your Qlik Sense Enterprise application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5924f-319">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="5924f-319">Additional resources</span></span>

* [<span data-ttu-id="5924f-320">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5924f-320">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5924f-321">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="5924f-321">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_203.png

[qs6]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_06.png
[qs7]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_07.png
[qs8]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_08.png
[qs9]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_09.png
[qs10]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_10.png
[qs11]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_11.png
[qs12]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_12.png
[qs13]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_13.png
[qs14]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_14.png
[qs15]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_15.png
[qs16]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_16.png
[qs17]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_17.png
[qs18]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_18.png
[qs19]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_19.png
[qs20]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_20.png
[qs24]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_24.png
[qs51]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_51.png
[qs52]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_52.png
[qs53]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_53.png

