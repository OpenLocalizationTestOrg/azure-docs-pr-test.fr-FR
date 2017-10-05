---
title: "Didacticiel : Intégration d’Azure Active Directory avec SAP Business Object Cloud | Microsoft Docs)"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et SAP Business Object Cloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 6c5e44f0-4e52-463f-b879-834d80a55cdf
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: 6d517c5e302ac36e5bba2053998c75f8f4d42683
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-object-cloud"></a><span data-ttu-id="efe73-103">Didacticiel : Intégration d’Azure Active Directory avec SAP Business Object Cloud</span><span class="sxs-lookup"><span data-stu-id="efe73-103">Tutorial: Azure Active Directory integration with SAP Business Object Cloud</span></span>

<span data-ttu-id="efe73-104">L’objectif de ce didacticiel est de vous apprendre à intégrer SAP Business Object Cloud avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="efe73-104">In this tutorial, you learn how to integrate SAP Business Object Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="efe73-105">Intégrer SAP Business Object Cloud avec Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="efe73-105">You get the following benefits when you integrate SAP Business Object Cloud with Azure AD:</span></span>

- <span data-ttu-id="efe73-106">Dans Azure AD, vous pouvez contrôler l’accès à SAP Business Object Cloud.</span><span class="sxs-lookup"><span data-stu-id="efe73-106">In Azure AD, you can control who has access to SAP Business Object Cloud.</span></span>
- <span data-ttu-id="efe73-107">Vous pouvez connecter automatiquement vos utilisateurs à SAP Business objet Cloud à l’aide de l’authentification unique et d’un compte utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="efe73-107">You can automatically sign in your users to SAP Business Object Cloud by using single sign-on and a user's Azure AD account.</span></span>
- <span data-ttu-id="efe73-108">Vous pouvez gérer vos comptes à un emplacement central : le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="efe73-108">You can manage your accounts in one, central location, the Azure portal.</span></span>

<span data-ttu-id="efe73-109">Pour en savoir plus sur l’intégration d’applications software as a service (SaaS) à Azure AD, consultez l’article [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="efe73-109">To learn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="efe73-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="efe73-110">Prerequisites</span></span>

<span data-ttu-id="efe73-111">Pour configurer l’intégration d’Azure AD à SAP Business Object Cloud, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="efe73-111">To set up Azure AD integration with SAP Business Object Cloud, you need the following items:</span></span>

- <span data-ttu-id="efe73-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="efe73-112">An Azure AD subscription</span></span>
- <span data-ttu-id="efe73-113">SAP Business Object Cloud pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="efe73-113">An SAP Business Object Cloud, with single sign-on turned on</span></span>

> [!NOTE]
> <span data-ttu-id="efe73-114">Lorsque vous testez les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="efe73-114">If you test the steps in this tutorial, we recommend that you don't test them in a production environment.</span></span>

<span data-ttu-id="efe73-115">Recommandations pour tester les étapes de ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="efe73-115">Recommendations for testing the steps in this tutorial:</span></span>

- <span data-ttu-id="efe73-116">N’utilisez pas votre environnement de production, à moins que cela ne soit nécessaire.</span><span class="sxs-lookup"><span data-stu-id="efe73-116">Do not use your production environment, unless it's necessary.</span></span>
- <span data-ttu-id="efe73-117">Si vous ne disposez pas d’un environnement d’essai Azure AD, vous pouvez [obtenir un essai gratuit d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="efe73-117">If you don't have an Azure AD trial environment, you can [get a one-month free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="efe73-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="efe73-118">Scenario description</span></span>
<span data-ttu-id="efe73-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="efe73-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="efe73-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="efe73-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="efe73-121">Ajoutez SAP Business Object Cloud depuis la galerie.</span><span class="sxs-lookup"><span data-stu-id="efe73-121">Add SAP Business Object Cloud from the gallery.</span></span>
2. <span data-ttu-id="efe73-122">Configurez et testez l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="efe73-122">Set up and test Azure AD single sign-on.</span></span>

## <a name="add-sap-business-object-cloud-from-the-gallery"></a><span data-ttu-id="efe73-123">Ajouter SAP Business Object Cloud depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="efe73-123">Add SAP Business Object Cloud from the gallery</span></span>
<span data-ttu-id="efe73-124">Pour configurer l’intégration de SAP Business Object Cloud à Azure AD, ajoutez SAP Business Object Cloud, disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="efe73-124">To set up the integration of SAP Business Object Cloud with Azure AD, in the gallery, add SAP Business Object Cloud to your list of managed SaaS apps.</span></span>

<span data-ttu-id="efe73-125">Pour ajouter SAP Business Object Cloud depuis la galerie :</span><span class="sxs-lookup"><span data-stu-id="efe73-125">To add SAP Business Object Cloud from the gallery:</span></span>

1. <span data-ttu-id="efe73-126">Dans le menu gauche du [Portail Azure](https://portal.azure.com), sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="efe73-126">In the [Azure portal](https://portal.azure.com), in the left menu, select **Azure Active Directory**.</span></span> 

    ![Bouton Azure Active Directory][1]

2. <span data-ttu-id="efe73-128">Sélectionnez **Applications d’entreprise**, puis **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="efe73-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Page Applications d’entreprise][2]
    
3. <span data-ttu-id="efe73-130">Pour ajouter une nouvelle application, sélectionnez **Nouvelle application**.</span><span class="sxs-lookup"><span data-stu-id="efe73-130">To add a new application, select **New application**.</span></span>

    ![Bouton Nouvelle application][3]

4. <span data-ttu-id="efe73-132">Dans la zone de recherche, entrez **SAP Business Object Cloud**.</span><span class="sxs-lookup"><span data-stu-id="efe73-132">In the search box, enter **SAP Business Object Cloud**.</span></span>

    ![La zone de recherche](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_search.png)

5. <span data-ttu-id="efe73-134">Dans le panneau de résultats, sélectionnez **SAP Business Object Cloud**, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="efe73-134">In the results panel, select **SAP Business Object Cloud**, and then select **Add**.</span></span>

    ![SAP Business Object Cloud dans la liste des résultats](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_addfromgallery.png)

##  <a name="set-up-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="efe73-136">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="efe73-136">Set up and test Azure AD single sign-on</span></span>

<span data-ttu-id="efe73-137">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec SAP Business Object Cloud, grâce à un utilisateur de test appelé *Britta Simon*.</span><span class="sxs-lookup"><span data-stu-id="efe73-137">In this section, you set up and test Azure AD single sign-on with SAP Business Object Cloud based on a test user named *Britta Simon*.</span></span>

<span data-ttu-id="efe73-138">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur SAP Business Object Cloud équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="efe73-138">For single sign-on to work, Azure AD needs to know the Azure AD counterpart user in SAP Business Object Cloud.</span></span> <span data-ttu-id="efe73-139">Il faut établir une relation entre un utilisateur Azure AD et l’utilisateur SAP Business Object Cloud associé.</span><span class="sxs-lookup"><span data-stu-id="efe73-139">A link relationship between an Azure AD user and the related user in SAP Business Object Cloud must be established.</span></span>

<span data-ttu-id="efe73-140">Pour établir une relation, dans SAP Business Object Cloud, assignez la valeur **Nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="efe73-140">To establish the link relationship, in SAP Business Object Cloud, for **Username**, assign the value of the **user name** in Azure AD.</span></span>

<span data-ttu-id="efe73-141">Pour configurer et tester l’authentification unique Azure AD avec SAP Business Object Cloud, vous devez exécuter les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="efe73-141">To configure and test Azure AD single sign-on with SAP Business Object Cloud, complete the following tasks:</span></span>

1. <span data-ttu-id="efe73-142">[Configurer l’authentification unique Azure AD](#set-up-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="efe73-142">[Set up Azure AD single sign-on](#set-up-azure-ad-single-sign-on).</span></span> <span data-ttu-id="efe73-143">Configure un utilisateur afin qu’il puisse utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="efe73-143">Sets up a user to use this feature.</span></span>
2. <span data-ttu-id="efe73-144">[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="efe73-144">[Create an Azure AD test user](#create-an-azure-ad-test-user).</span></span> <span data-ttu-id="efe73-145">Teste l’authentification unique Azure AD avec l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="efe73-145">Tests Azure AD single sign-on with the user Britta Simon.</span></span>
3. <span data-ttu-id="efe73-146">[Créer un utilisateur de test pour SAP Business Object Cloud](#create-an-sap-business-object-cloud-test-user).</span><span class="sxs-lookup"><span data-stu-id="efe73-146">[Create an SAP Business Object Cloud test user](#create-an-sap-business-object-cloud-test-user).</span></span> <span data-ttu-id="efe73-147">Crée un équivalent de Britta Simon dans SAP Business Object Cloud lié à la représentation d’un utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="efe73-147">Creates a counterpart of Britta Simon in SAP Business Object Cloud that is linked to the Azure AD representation of the user.</span></span>
4. <span data-ttu-id="efe73-148">[Attribuer l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user).</span><span class="sxs-lookup"><span data-stu-id="efe73-148">[Assign the Azure AD test user](#assign-the-azure-ad-test-user).</span></span> <span data-ttu-id="efe73-149">Configure Britta Simon afin qu’elle puisse utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="efe73-149">Sets up Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="efe73-150">[Tester l’authentification unique](#test-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="efe73-150">[Test single sign-on](#test-single-sign-on).</span></span> <span data-ttu-id="efe73-151">Vérifie que la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="efe73-151">Verifies that the configuration works.</span></span>

### <a name="set-up-azure-ad-single-sign-on"></a><span data-ttu-id="efe73-152">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="efe73-152">Set up Azure AD single sign-on</span></span>

<span data-ttu-id="efe73-153">Dans cette section, activez l’authentification unique Azure AD dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="efe73-153">In this section, you turn on Azure AD single sign-on in the Azure portal.</span></span> <span data-ttu-id="efe73-154">Ensuite, configurez l’authentification unique dans votre application SAP Business objet Cloud.</span><span class="sxs-lookup"><span data-stu-id="efe73-154">Then, you set up single sign-on in your SAP Business Object Cloud application.</span></span>

<span data-ttu-id="efe73-155">Pour configurer l’authentification Azure AD avec SAP Business objet Cloud :</span><span class="sxs-lookup"><span data-stu-id="efe73-155">To set up Azure AD single sign-on with SAP Business Object Cloud:</span></span>

1. <span data-ttu-id="efe73-156">Dans le portail Azure, dans la page d’intégration de l’application **SAP Business Object Cloud**, sélectionnez **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="efe73-156">In the Azure portal, on the **SAP Business Object Cloud** application integration page, select **Single sign-on**.</span></span>

    ![Sélectionner l’authentification unique][4]

2. <span data-ttu-id="efe73-158">Dans la page **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML**.</span><span class="sxs-lookup"><span data-stu-id="efe73-158">On the **Single sign-on** page, for **Mode**, select **SAML-based Sign-on**.</span></span>
 
    ![Sélectionner l’authentification basée sur SAML](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_samlbase.png)

3. <span data-ttu-id="efe73-160">Dans la section **Domaine et URL SAP Business Object Cloud**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="efe73-160">Under **SAP Business Object Cloud Domain and URLs**, complete the following steps:</span></span>

    1. <span data-ttu-id="efe73-161">Dans la boîte **URL de connexion**, tapez une URL dont le modèle est le suivant :</span><span class="sxs-lookup"><span data-stu-id="efe73-161">In the **Sign-on URL** box, enter a URL that has the following pattern:</span></span> 
    | |
    |-|-|
    | `https://<sub-domain>.sapanalytics.cloud/` |
    | `https://<sub-domain>.sapbusinessobjects.cloud/` |

    2. <span data-ttu-id="efe73-162">Dans la boîte **Identificateur**, tapez une URL dont le modèle est le suivant :</span><span class="sxs-lookup"><span data-stu-id="efe73-162">In the **Identifier** box, enter a URL that has the following pattern:</span></span>
    | |
    |-|-|
    | `<sub-domain>.sapbusinessobjects.cloud` |
    | `<sub-domain>.sapanalytics.cloud` |

    ![URL de la page URL et domaine SAP Business Object Cloud](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_url.png)
 
    > [!NOTE] 
    > <span data-ttu-id="efe73-164">Les valeurs de ces URL sont uniquement à des fins de démonstration.</span><span class="sxs-lookup"><span data-stu-id="efe73-164">The values in these URLs are for demonstration only.</span></span> <span data-ttu-id="efe73-165">Mettez à jour les valeurs avec les URL de connexion et de l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="efe73-165">Update the values with the actual sign-on URL and identifier URL.</span></span> <span data-ttu-id="efe73-166">Pour obtenir l’URL de connexion, contactez [l’équipe de support technique SAP Business Object Cloud Client](https://www.sap.com/product/analytics/cloud-analytics.support.html).</span><span class="sxs-lookup"><span data-stu-id="efe73-166">To get the sign-on URL, contact the [SAP Business Object Cloud Client support team](https://www.sap.com/product/analytics/cloud-analytics.support.html).</span></span> <span data-ttu-id="efe73-167">Vous pouvez obtenir l’URL de l’identificateur en téléchargeant les métadonnées SAP Business Object Cloud depuis la console d’administration.</span><span class="sxs-lookup"><span data-stu-id="efe73-167">You can get the identifier URL by downloading the SAP Business Object Cloud metadata from the admin console.</span></span> <span data-ttu-id="efe73-168">Une explication sera fournie plus loin dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="efe73-168">This is explained later in the tutorial.</span></span> 

4. <span data-ttu-id="efe73-169">Sous **le certificat de signature SAML**, sélectionnez **XML des métadonnées**.</span><span class="sxs-lookup"><span data-stu-id="efe73-169">Under **SAML Signing Certificate**, select **Metadata XML**.</span></span> <span data-ttu-id="efe73-170">Ensuite, enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="efe73-170">Then, save the metadata file on your computer.</span></span>

    ![Sélectionnez XML des métadonnées](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_certificate.png) 

5. <span data-ttu-id="efe73-172">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="efe73-172">Select **Save**.</span></span>

    ![Sélectionner Enregistrer](./media/active-directory-saas-sapboc-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="efe73-174">Dans une autre fenêtre du navigateur Web, ouvrez une session sur votre site d’entreprise SAP Business Object Cloud en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="efe73-174">In a different web browser window, sign in to your SAP Business Object Cloud company site as an administrator.</span></span>

7. <span data-ttu-id="efe73-175">Sélectionnez **Menu** > **Système** > **Administration**.</span><span class="sxs-lookup"><span data-stu-id="efe73-175">Select **Menu** > **System** > **Administration**.</span></span>
    
    ![Sélectionner Menu, puis Système et Administration](./media/active-directory-saas-sapboc-tutorial/config1.png)

8. <span data-ttu-id="efe73-177">Sous l’onglet **Sécurité**, sélectionnez l’icône (stylet) **Modifier**.</span><span class="sxs-lookup"><span data-stu-id="efe73-177">On the **Security** tab, select the **Edit** (pen) icon.</span></span>
    
    ![Sous l’onglet Sécurité, sélectionner l’icône Modifier](./media/active-directory-saas-sapboc-tutorial/config2.png)  

9. <span data-ttu-id="efe73-179">Sélectionnez **Méthode d’authentification unique SAML (SSO)** comme **Méthode d’authentification**.</span><span class="sxs-lookup"><span data-stu-id="efe73-179">For **Authentication Method**, select **SAML Single Sign-On (SSO)**.</span></span>

    ![Sélectionner Authentification unique SAML comme méthode d’authentification](./media/active-directory-saas-sapboc-tutorial/config3.png)  

10. <span data-ttu-id="efe73-181">Pour télécharger les métadonnées du fournisseur de services (étape 1), sélectionnez **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="efe73-181">To download the service provider metadata (Step 1), select **Download**.</span></span> <span data-ttu-id="efe73-182">Dans le fichier de métadonnées, recherchez et copiez la valeur **entityID**.</span><span class="sxs-lookup"><span data-stu-id="efe73-182">In the metadata file, find and copy the **entityID** value.</span></span> <span data-ttu-id="efe73-183">Dans le portail Azure, sous **URL et domaine SAP Business Object Cloud**, collez la valeur dans la boîte **Identificateur**.</span><span class="sxs-lookup"><span data-stu-id="efe73-183">In the Azure portal, under **SAP Business Object Cloud Domain and URLs**, paste the value in the **Identifier** box.</span></span>

    ![Copier et coller la valeur entityID](./media/active-directory-saas-sapboc-tutorial/config4.png)  

11. <span data-ttu-id="efe73-185">Pour télécharger les métadonnées du fournisseur de services (étape 2) dans le fichier que vous avez téléchargé depuis le portail Azure, sous **Charger les métadonnées du fournisseur d’identité**, sélectionnez **Charger**.</span><span class="sxs-lookup"><span data-stu-id="efe73-185">To upload the service provider metadata (Step 2) in the file that you downloaded from the Azure portal, under **Upload Identity Provider metadata**, select **Upload**.</span></span>  

    ![Sous Charger les métadonnées du fournisseur d’identité, sélectionnez Charger](./media/active-directory-saas-sapboc-tutorial/config5.png)

12. <span data-ttu-id="efe73-187">Dans la liste **Attribut utilisateur**, sélectionnez l’attribut utilisateur (étape 3) que vous souhaitez utiliser pour votre mise en œuvre.</span><span class="sxs-lookup"><span data-stu-id="efe73-187">In the **User Attribute** list, select the user attribute (Step 3) that you want to use for your implementation.</span></span> <span data-ttu-id="efe73-188">Cet attribut utilisateur est mappé au fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="efe73-188">This user attribute maps to the identity provider.</span></span> <span data-ttu-id="efe73-189">Pour entrer un attribut personnalisé sur la page de l’utilisateur, utilisez l’option **Mappage SAML personnalisé**.</span><span class="sxs-lookup"><span data-stu-id="efe73-189">To enter a custom attribute on the user's page, use the **Custom SAML Mapping** option.</span></span> <span data-ttu-id="efe73-190">Ou bien, vous pouvez sélectionner **E-mail** ou **ID UTILISATEUR** en tant qu’attribut utilisateur.</span><span class="sxs-lookup"><span data-stu-id="efe73-190">Or, you can select either **Email** or **USER ID** as the user attribute.</span></span> <span data-ttu-id="efe73-191">Dans notre exemple, nous avons sélectionné **E-mail**, car nous avons mappé la revendication de l’identificateur d’utilisateur avec l’attribut **userprincipalname** dans la section **attributs utilisateur** dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="efe73-191">In our example, we selected **Email** because we mapped the user identifier claim with the **userprincipalname** attribute in the **User Attributes** section in the Azure portal.</span></span> <span data-ttu-id="efe73-192">Cela fournit un e-mail de l’utilisateur unique, qui est envoyé à l’application SAP Business Object Cloud dans chaque réponse SAML correcte.</span><span class="sxs-lookup"><span data-stu-id="efe73-192">This provides a unique user email, which is sent to the SAP Business Object Cloud application in every successful SAML response.</span></span>

    ![Sélectionner un attribut utilisateur](./media/active-directory-saas-sapboc-tutorial/config6.png)

13. <span data-ttu-id="efe73-194">Pour vérifier le compte avec le fournisseur d’identité (étape 4), dans la boîte **Informations d’identification de connexion (e-mail)**, entrez l’adresse e-mail de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="efe73-194">To verify the account with the identity provider (Step 4), in the **Login Credential (Email)** box, enter the user's email address.</span></span> <span data-ttu-id="efe73-195">Ensuite, sélectionnez **Vérifier le compte**.</span><span class="sxs-lookup"><span data-stu-id="efe73-195">Then, select **Verify Account**.</span></span> <span data-ttu-id="efe73-196">Le système ajoute les informations d’identification de connexion au compte utilisateur.</span><span class="sxs-lookup"><span data-stu-id="efe73-196">The system adds sign-in credentials to the user account.</span></span>

    ![Entrer l’e-mail et sélectionner Vérifier le compte](./media/active-directory-saas-sapboc-tutorial/config7.png)

14. <span data-ttu-id="efe73-198">Sélectionnez l’icône **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="efe73-198">Select the **Save** icon.</span></span>

    ![Icône Enregistrer](./media/active-directory-saas-sapboc-tutorial/save.png)

> [!TIP]
> <span data-ttu-id="efe73-200">Vous pouvez lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez votre application !</span><span class="sxs-lookup"><span data-stu-id="efe73-200">You can read a concise version of these instructions in the [Azure portal](https://portal.azure.com), while you are setting up your app!</span></span> <span data-ttu-id="efe73-201">Après avoir ajouté l’application en sélectionnant **Active Directory** > **Applications d’entreprise**, sélectionnez l’onglet **Authentification unique**. Vous pouvez accéder à la documentation incorporée dans la section **Configuration** en bas de la page.</span><span class="sxs-lookup"><span data-stu-id="efe73-201">After you add the app by selecting **Active Directory** > **Enterprise Applications**, select the **Single Sign-On** tab. You can access the embedded documentation in the **Configuration** section, at the bottom of the page.</span></span> <span data-ttu-id="efe73-202">Pour plus d’informations, consultez la page [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="efe73-202">For more information, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="efe73-203">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="efe73-203">Create an Azure AD test user</span></span>
<span data-ttu-id="efe73-204">Dans cette section, créez un utilisateur de test nommé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="efe73-204">In this section, you create a test user named Britta Simon in the Azure portal.</span></span>

<span data-ttu-id="efe73-205">Pour créer un utilisateur de test dans Azure AD :</span><span class="sxs-lookup"><span data-stu-id="efe73-205">To create a test user in Azure AD:</span></span>

1. <span data-ttu-id="efe73-206">Dans le menu de gauche du Portail Azure, sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="efe73-206">In the Azure portal, in the left menu, select **Azure Active Directory**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sapboc-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="efe73-208">Pour afficher la liste des utilisateurs, sélectionnez **Utilisateurs et groupes**, puis **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="efe73-208">To display the list of users, select **Users and groups**, and then select **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sapboc-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="efe73-210">Pour ouvrir la boîte de dialogue **Utilisateur**, sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="efe73-210">To open the **User** dialog box, select **Add**.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sapboc-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="efe73-212">Dans la boîte de dialogue **Utilisateur**, suivez les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="efe73-212">In the **User** dialog box, complete the following steps:</span></span>
 
    1. <span data-ttu-id="efe73-213">Dans la boîte **Nom**, tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="efe73-213">In the **Name** box, enter **BrittaSimon**.</span></span>

    2. <span data-ttu-id="efe73-214">Dans la boîte **Nom d’utilisateur**, tapez l’adresse e-mail de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="efe73-214">In the **User name** box, enter the email address of the user Britta Simon.</span></span>

    3. <span data-ttu-id="efe73-215">Cochez la case **Afficher le mot de passe**, puis notez la valeur affichée dans le champ **Mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="efe73-215">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    4. <span data-ttu-id="efe73-216">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="efe73-216">Select **Create**.</span></span>

        ![Boîte de dialogue Utilisateur](./media/active-directory-saas-sapboc-tutorial/create_aaduser_04.png) 

    ![Créer un utilisateur Azure AD][100]

### <a name="create-an-sap-business-object-cloud-test-user"></a><span data-ttu-id="efe73-219">Créer un utilisateur de test SAP Business Object Cloud</span><span class="sxs-lookup"><span data-stu-id="efe73-219">Create an SAP Business Object Cloud test user</span></span>

<span data-ttu-id="efe73-220">Les utilisateurs Azure AD doivent être approvisionnés dans SAP Business Object Cloud avant de pouvoir se connecter à SAP Business Object Cloud.</span><span class="sxs-lookup"><span data-stu-id="efe73-220">Azure AD users must be provisioned in SAP Business Object Cloud before they can sign in to SAP Business Object Cloud.</span></span> <span data-ttu-id="efe73-221">Dans SAP Business Object Cloud, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="efe73-221">In SAP Business Object Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="efe73-222">Pour approvisionner un compte d’utilisateur :</span><span class="sxs-lookup"><span data-stu-id="efe73-222">To provision a user account:</span></span>

1. <span data-ttu-id="efe73-223">Connectez-vous en tant qu’administrateur à votre site d’entreprise SAP Business Object Cloud.</span><span class="sxs-lookup"><span data-stu-id="efe73-223">Sign in to your SAP Business Object Cloud company site as an administrator.</span></span>

2. <span data-ttu-id="efe73-224">Sélectionnez **Menu** > **Sécurité** > **Utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="efe73-224">Select **Menu** > **Security** > **Users**.</span></span>

    ![Ajouter un employé](./media/active-directory-saas-sapboc-tutorial/user1.png)

3. <span data-ttu-id="efe73-226">Sur la page **Utilisateurs**, pour ajouter de nouvelles informations de l’utilisateur, sélectionnez **+**.</span><span class="sxs-lookup"><span data-stu-id="efe73-226">On the **Users** page, to add new user details, select **+**.</span></span> 

    ![Page Ajouter des utilisateurs](./media/active-directory-saas-sapboc-tutorial/user4.png)

    <span data-ttu-id="efe73-228">Effectuez ensuite les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="efe73-228">Then, complete the following steps:</span></span>

    1. <span data-ttu-id="efe73-229">Dans la boîte **ID UTILISATEUR**, entrez l’ID utilisateur de l’utilisateur, par exemple **Britta**.</span><span class="sxs-lookup"><span data-stu-id="efe73-229">In the **USER ID** box, enter the user ID of the user, like **Britta**.</span></span>

    2. <span data-ttu-id="efe73-230">Dans la boîte **PRÉNOM**, entrez le prénom de l’utilisateur, par exemple **Britta**.</span><span class="sxs-lookup"><span data-stu-id="efe73-230">In the **FIRST NAME** box, enter the first name of the user, like **Britta**.</span></span>

    3. <span data-ttu-id="efe73-231">Dans la boîte **NOM**, entrez le prénom de l’utilisateur, par exemple **Simon**.</span><span class="sxs-lookup"><span data-stu-id="efe73-231">In the **LAST NAME** box, enter the last name of the user, like **Simon**.</span></span>

    4. <span data-ttu-id="efe73-232">Dans la boîte **NOM COMPLET**, tapez le nom complet de l’utilisateur, par exemple **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="efe73-232">In the **DISPLAY NAME** box, enter the full name of the user, like **Britta Simon**.</span></span>

    5. <span data-ttu-id="efe73-233">Dans la boîte **E-MAIL**, entrez l’adresse e-mail de l’utilisateur, par exemple **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="efe73-233">In the **E-MAIL** box, enter the email address of the user, like **brittasimon@contoso.com**.</span></span>

    6. <span data-ttu-id="efe73-234">Dans la page **Sélectionner des rôles**, sélectionnez le rôle approprié pour l’utilisateur, puis **OK**.</span><span class="sxs-lookup"><span data-stu-id="efe73-234">On the **Select Roles** page, select the appropriate role for the user, and then select **OK**.</span></span>

      ![Sélectionner un rôle](./media/active-directory-saas-sapboc-tutorial/user3.png)

    7. <span data-ttu-id="efe73-236">Sélectionnez l’icône **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="efe73-236">Select the **Save** icon.</span></span>    


### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="efe73-237">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="efe73-237">Assign the Azure AD test user</span></span>

<span data-ttu-id="efe73-238">Dans cette section, autorisez l’utilisateur Britta Simon à utiliser l’authentification unique Azure AD en lui accordant l’accès utilisateur à SAP Business Object Cloud.</span><span class="sxs-lookup"><span data-stu-id="efe73-238">In this section, you allow the user Britta Simon to use Azure AD single sign-on by granting the user account access to SAP Business Object Cloud.</span></span>

<span data-ttu-id="efe73-239">Pour assigner Britta Simon à SAP Business Object Cloud :</span><span class="sxs-lookup"><span data-stu-id="efe73-239">To assign Britta Simon to SAP Business Object Cloud:</span></span>

1. <span data-ttu-id="efe73-240">Sur le Portail Azure, ouvrez l’affichage des applications, puis accédez à l’affichage des répertoires.</span><span class="sxs-lookup"><span data-stu-id="efe73-240">In the Azure portal, open the applications view, and then go to the directory view.</span></span> <span data-ttu-id="efe73-241">Sélectionnez **Applications d’entreprise**, puis **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="efe73-241">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="efe73-243">Dans la liste des applications, sélectionnez **SAP Business Object Cloud**.</span><span class="sxs-lookup"><span data-stu-id="efe73-243">In the applications list, select **SAP Business Object Cloud**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_app.png) 

3. <span data-ttu-id="efe73-245">Dans le menu de gauche, sélectionnez **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="efe73-245">In the left menu, select **Users and groups**.</span></span>

    ![Sélectionner Utilisateurs et groupes][202] 

4. <span data-ttu-id="efe73-247">Sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="efe73-247">Select **Add**.</span></span> <span data-ttu-id="efe73-248">Ensuite, sur la page **Ajouter une affectation**, sélectionnez **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="efe73-248">Then, on the **Add Assignment** page, select **Users and groups**.</span></span>

    ![La page Ajouter une attribution][203]

5. <span data-ttu-id="efe73-250">Dans la page **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="efe73-250">On the **Users and groups** page, in the list of users, select **Britta Simon**.</span></span>

6. <span data-ttu-id="efe73-251">Sur la page **Utilisateurs et groupes**, sélectionnez **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="efe73-251">On the **Users and groups** page, select **Select**.</span></span>

7. <span data-ttu-id="efe73-252">Sur la page **Ajouter une affectation**, sélectionnez **Affecter**.</span><span class="sxs-lookup"><span data-stu-id="efe73-252">On the **Add Assignment** page, select **Assign**.</span></span>

![Attribuer le rôle utilisateur][200] 
    
### <a name="test-single-sign-on"></a><span data-ttu-id="efe73-254">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="efe73-254">Test single sign-on</span></span>

<span data-ttu-id="efe73-255">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="efe73-255">In this section, you test your Azure AD single sign-on configuration by using the access panel.</span></span>

<span data-ttu-id="efe73-256">En cliquant sur la vignette SAP Business Object Cloud dans le panneau d’accès, vous êtes automatiquement connecté à votre application SAP Business Object Cloud.</span><span class="sxs-lookup"><span data-stu-id="efe73-256">When you select the SAP Business Object Cloud tile in the access panel, you should be automatically signed in to your SAP Business Object Cloud application.</span></span>

<span data-ttu-id="efe73-257">Pour plus d’informations sur le volet d’accès, consultez la page [Présentation du volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="efe73-257">For more information about the access panel, see [Introduction to the access panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="efe73-258">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="efe73-258">Additional resources</span></span>

* [<span data-ttu-id="efe73-259">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="efe73-259">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="efe73-260">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="efe73-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_203.png

