---
title: "Didacticiel : Intégration d’Azure Active Directory à Zscaler Private Access (ZPA) | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Zscaler Private Access (ZPA)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 83711115-1c4f-4dd7-907b-3da24b37c89e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jeedes
ms.openlocfilehash: 5c598bfa5b6725d21a89df54dbcb3314cc631d80
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-private-access-zpa"></a><span data-ttu-id="c9425-103">Didacticiel : Intégration d’Azure Active Directory à Zscaler Private Access (ZPA)</span><span class="sxs-lookup"><span data-stu-id="c9425-103">Tutorial: Azure Active Directory integration with Zscaler Private Access (ZPA)</span></span>

<span data-ttu-id="c9425-104">Dans ce didacticiel, vous allez apprendre à intégrer Zscaler Private Access (ZPA) à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c9425-104">In this tutorial, you learn how to integrate Zscaler Private Access (ZPA) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c9425-105">L’intégration de Zscaler Private Access (ZPA) dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="c9425-105">Integrating Zscaler Private Access (ZPA) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c9425-106">Dans Azure AD, vous pouvez contrôler qui a accès à Zscaler Private Access (ZPA)</span><span class="sxs-lookup"><span data-stu-id="c9425-106">You can control in Azure AD who has access to Zscaler Private Access (ZPA)</span></span>
- <span data-ttu-id="c9425-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Zscaler Private Access (ZPA) (via l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9425-107">You can enable your users to automatically get signed-on to Zscaler Private Access (ZPA) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c9425-108">Vous pouvez gérer vos comptes de manière centralisée dans le portail de gestion Azure.</span><span class="sxs-lookup"><span data-stu-id="c9425-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="c9425-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c9425-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c9425-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c9425-110">Prerequisites</span></span>

<span data-ttu-id="c9425-111">Pour configurer l’intégration d’Azure AD à Zscaler Private Access (ZPA), vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="c9425-111">To configure Azure AD integration with Zscaler Private Access (ZPA), you need the following items:</span></span>

- <span data-ttu-id="c9425-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9425-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c9425-113">Un abonnement Zscaler Private Access (ZPA) activé via l’authentification unique (SSO)</span><span class="sxs-lookup"><span data-stu-id="c9425-113">A Zscaler Private Access (ZPA) single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="c9425-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="c9425-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="c9425-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="c9425-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c9425-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="c9425-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="c9425-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c9425-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="c9425-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="c9425-118">Scenario description</span></span>
<span data-ttu-id="c9425-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="c9425-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c9425-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="c9425-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c9425-121">Ajout de Zscaler Private Access (ZPA) à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="c9425-121">Adding Zscaler Private Access (ZPA) from the gallery</span></span>
2. <span data-ttu-id="c9425-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9425-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-zscaler-private-access-zpa-from-the-gallery"></a><span data-ttu-id="c9425-123">Ajout de Zscaler Private Access (ZPA) à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="c9425-123">Adding Zscaler Private Access (ZPA) from the gallery</span></span>
<span data-ttu-id="c9425-124">Pour configurer l’intégration de Zscaler Private Access (ZPA) à Azure AD, vous devez ajouter Zscaler Private Access (ZPA) à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="c9425-124">To configure the integration of Zscaler Private Access (ZPA) into Azure AD, you need to add Zscaler Private Access (ZPA) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c9425-125">**Pour ajouter Zscaler Private Access (ZPA) à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c9425-125">**To add Zscaler Private Access (ZPA) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c9425-126">Dans le panneau de navigation gauche du **[Portail de gestion Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c9425-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c9425-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="c9425-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c9425-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="c9425-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="c9425-131">Cliquez sur le bouton **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="c9425-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="c9425-133">Dans la zone de recherche, tapez **Zscaler Private Access (ZPA)**.</span><span class="sxs-lookup"><span data-stu-id="c9425-133">In the search box, type **Zscaler Private Access (ZPA)**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_001.png)

5. <span data-ttu-id="c9425-135">Dans le volet de résultats, sélectionnez **Zscaler Private Access (ZPA)**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="c9425-135">In the results panel, select **Zscaler Private Access (ZPA)**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c9425-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9425-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c9425-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Zscaler Private Access (ZPA) avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="c9425-138">In this section, you configure and test Azure AD single sign-on with Zscaler Private Access (ZPA) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c9425-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Zscaler Private Access (ZPA) équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c9425-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Zscaler Private Access (ZPA) is to a user in Azure AD.</span></span> <span data-ttu-id="c9425-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Zscaler Private Access (ZPA) associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="c9425-140">In other words, a link relationship between an Azure AD user and the related user in Zscaler Private Access (ZPA) needs to be established.</span></span>

<span data-ttu-id="c9425-141">Pour cela, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** dans Zscaler Private Access (ZPA).</span><span class="sxs-lookup"><span data-stu-id="c9425-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Zscaler Private Access (ZPA).</span></span>

<span data-ttu-id="c9425-142">Pour configurer et tester l'authentification unique Azure AD avec Zscaler Private Access (ZPA), vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="c9425-142">To configure and test Azure AD single sign-on with Zscaler Private Access (ZPA), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c9425-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="c9425-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c9425-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c9425-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c9425-145">**[Création d'un utilisateur de test Zscaler Private Access (ZPA)](#creating-a-zscaler-private-access-(zpa)-test-user)** pour avoir un équivalent de Zscaler Private Access (ZPA) Simon dans Moxtra lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="c9425-145">**[Creating a Zscaler Private Access (ZPA) test user](#creating-a-zscaler-private-access-(zpa)-test-user)** - to have a counterpart of Britta Simon in Zscaler Private Access (ZPA) that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="c9425-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c9425-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c9425-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="c9425-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c9425-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9425-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c9425-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail de gestion Azure et configurer l’authentification unique dans votre application Zscaler Private Access (ZPA).</span><span class="sxs-lookup"><span data-stu-id="c9425-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Zscaler Private Access (ZPA) application.</span></span>

<span data-ttu-id="c9425-150">**Pour configurer l’authentification unique Azure AD avec Zscaler Private Access (ZPA), procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c9425-150">**To configure Azure AD single sign-on with Zscaler Private Access (ZPA), perform the following steps:**</span></span>

1. <span data-ttu-id="c9425-151">Dans le portail de gestion Azure, sur la page d’intégration de l’application **Zscaler Private Access (ZPA)**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="c9425-151">In the Azure Management portal, on the **Zscaler Private Access (ZPA)** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="c9425-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="c9425-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_300.png)
    
3. <span data-ttu-id="c9425-155">Dans la section **Domaine et URL Zscaler Private Access (ZPA)**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c9425-155">On the **Zscaler Private Access (ZPA) Domain and URLs** section, perform the following steps:</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_01.png)

    <span data-ttu-id="c9425-157">a.</span><span class="sxs-lookup"><span data-stu-id="c9425-157">a.</span></span> <span data-ttu-id="c9425-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://samlsp.private.zscaler.com/auth/login?domain=<your-domain-name>`</span><span class="sxs-lookup"><span data-stu-id="c9425-158">In the **Sign On URL** textbox, type a URL using the following pattern: `https://samlsp.private.zscaler.com/auth/login?domain=<your-domain-name>`</span></span>

    <span data-ttu-id="c9425-159">b.</span><span class="sxs-lookup"><span data-stu-id="c9425-159">b.</span></span> <span data-ttu-id="c9425-160">Dans la zone de texte **Identificateur**, tapez : `https://samlsp.private.zscaler.com/auth/metadata`</span><span class="sxs-lookup"><span data-stu-id="c9425-160">In the **Identifier** textbox, type: `https://samlsp.private.zscaler.com/auth/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c9425-161">Notez qu’il ne s’agit pas des valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="c9425-161">Please note that these are not the real values.</span></span> <span data-ttu-id="c9425-162">Vous devez mettre à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="c9425-162">You have to update these values with the actual Sign On URL and Identifier.</span></span> <span data-ttu-id="c9425-163">Nous vous suggérons d’utiliser ici la valeur d’URL unique dans l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="c9425-163">Here we suggest you to use the unique value of URL in the Identifier.</span></span> <span data-ttu-id="c9425-164">Contactez [l’équipe de support technique Zscaler Private Access (ZPA)](https://help.zscaler.com/zpa-submit-ticket) pour obtenir ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="c9425-164">Contact [Zscaler Private Access (ZPA) support team](https://help.zscaler.com/zpa-submit-ticket) to get these values.</span></span>

4. <span data-ttu-id="c9425-165">Dans la section **Certificat de signature SAML**, cliquez sur **Créer un certificat**.</span><span class="sxs-lookup"><span data-stu-id="c9425-165">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_400.png)   

5. <span data-ttu-id="c9425-167">Dans la boîte de dialogue **Créer un certificat**, cliquez sur l’icône de calendrier et sélectionnez une **date d’expiration**.</span><span class="sxs-lookup"><span data-stu-id="c9425-167">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="c9425-168">Ensuite, cliquez sur le bouton **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="c9425-168">Then click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_500.png)

6. <span data-ttu-id="c9425-170">Dans la section **Certificat de signature SAML**, sélectionnez **Activer le nouveau certificat** et cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="c9425-170">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_02.png)

7. <span data-ttu-id="c9425-172">Dans la fenêtre contextuelle **Certificat de substitution**, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="c9425-172">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_600.png)

8. <span data-ttu-id="c9425-174">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="c9425-174">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_03.png) 

9. <span data-ttu-id="c9425-176">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Zscaler Private Access (ZPA) en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="c9425-176">In a different web browser window, log into your Zscaler Private Access (ZPA) company site as an administrator.</span></span>

10. <span data-ttu-id="c9425-177">Accédez à **Administrateur**, puis cliquez sur **Configuration Idp**.</span><span class="sxs-lookup"><span data-stu-id="c9425-177">Navigate to **Administrator** and then click **Idp Configuration**.</span></span>

    ![Configurer l’authentification unique côté application](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_04.png)

11. <span data-ttu-id="c9425-179">Dans la section **Configuration Idp**, cliquez sur **Ajouter une nouvelle configuration IDP**.</span><span class="sxs-lookup"><span data-stu-id="c9425-179">In the **Idp Configuration** section, click **Add New IDP Configuration**.</span></span>

    ![Configurer l’authentification unique côté application](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_05.png)

12. <span data-ttu-id="c9425-181">Dans la section **Nouvelle configuration IDP**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c9425-181">In the **New IDP Configuration** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique côté application](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_06.png)

    <span data-ttu-id="c9425-183">a.</span><span class="sxs-lookup"><span data-stu-id="c9425-183">a.</span></span> <span data-ttu-id="c9425-184">Cliquez sur **Sélectionner un fichier** et chargez votre fichier de métadonnées téléchargé.</span><span class="sxs-lookup"><span data-stu-id="c9425-184">Click **Select File** and upload your downloaded metadata file.</span></span>

    <span data-ttu-id="c9425-185">b.</span><span class="sxs-lookup"><span data-stu-id="c9425-185">b.</span></span> <span data-ttu-id="c9425-186">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="c9425-186">Click **Save** button.</span></span>
    


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c9425-187">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9425-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="c9425-188">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le Portail de gestion Azure.</span><span class="sxs-lookup"><span data-stu-id="c9425-188">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="c9425-190">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c9425-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c9425-191">Dans le panneau de navigation gauche du **Portail de gestion Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c9425-191">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c9425-193">Accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs** pour afficher la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="c9425-193">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c9425-195">En haut de la boîte de dialogue, cliquez sur **Ajouter** pour ouvrir la boîte de dialogue **Utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="c9425-195">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c9425-197">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c9425-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c9425-199">a.</span><span class="sxs-lookup"><span data-stu-id="c9425-199">a.</span></span> <span data-ttu-id="c9425-200">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c9425-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c9425-201">b.</span><span class="sxs-lookup"><span data-stu-id="c9425-201">b.</span></span> <span data-ttu-id="c9425-202">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c9425-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c9425-203">c.</span><span class="sxs-lookup"><span data-stu-id="c9425-203">c.</span></span> <span data-ttu-id="c9425-204">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="c9425-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c9425-205">d.</span><span class="sxs-lookup"><span data-stu-id="c9425-205">d.</span></span> <span data-ttu-id="c9425-206">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="c9425-206">Click **Create**.</span></span> 



### <a name="creating-a-zscaler-private-access-zpa-test-user"></a><span data-ttu-id="c9425-207">Création d’un utilisateur de test Zscaler Private Access (ZPA)</span><span class="sxs-lookup"><span data-stu-id="c9425-207">Creating a Zscaler Private Access (ZPA) test user</span></span>

<span data-ttu-id="c9425-208">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Zscaler Private Access (ZPA).</span><span class="sxs-lookup"><span data-stu-id="c9425-208">In this section, you create a user called Britta Simon in Zscaler Private Access (ZPA).</span></span> <span data-ttu-id="c9425-209">Collaborez avec [l’équipe de support technique Zscaler Private Access (ZPA)](https://help.zscaler.com/zpa-submit-ticket) pour ajouter les utilisateurs dans la plate-forme Zscaler Private Access (ZPA).</span><span class="sxs-lookup"><span data-stu-id="c9425-209">Please work with [Zscaler Private Access (ZPA) support team](https://help.zscaler.com/zpa-submit-ticket) to add the users in the Zscaler Private Access (ZPA) platform.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c9425-210">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9425-210">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c9425-211">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Zscaler Private Access (ZPA).</span><span class="sxs-lookup"><span data-stu-id="c9425-211">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Zscaler Private Access (ZPA).</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="c9425-213">**Pour affecter Britta Simon à Zscaler Private Access (ZPA), procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="c9425-213">**To assign Britta Simon to Zscaler Private Access (ZPA), perform the following steps:**</span></span>

1. <span data-ttu-id="c9425-214">Dans le Portail de gestion Azure, ouvrez la vue des applications, accédez à la vue des répertoires, allez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="c9425-214">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="c9425-216">Dans la liste des applications, sélectionnez **Zscaler Private Access (ZPA)**.</span><span class="sxs-lookup"><span data-stu-id="c9425-216">In the applications list, select **Zscaler Private Access (ZPA)**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_50.png) 

3. <span data-ttu-id="c9425-218">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="c9425-218">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="c9425-220">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="c9425-220">Click **Add** button.</span></span> <span data-ttu-id="c9425-221">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="c9425-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="c9425-223">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="c9425-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c9425-224">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="c9425-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c9425-225">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="c9425-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="c9425-226">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="c9425-226">Testing single sign-on</span></span>

<span data-ttu-id="c9425-227">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="c9425-227">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c9425-228">Lorsque vous cliquez sur la mosaïque Zscaler Private Access (ZPA) dans le volet d'accès, vous êtes connecté automatiquement à votre application Zscaler Private Access (ZPA).</span><span class="sxs-lookup"><span data-stu-id="c9425-228">When you click the Zscaler Private Access (ZPA) tile in the Access Panel, you should get automatically signed-on to your Zscaler Private Access (ZPA) application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="c9425-229">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="c9425-229">Additional resources</span></span>

* [<span data-ttu-id="c9425-230">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c9425-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c9425-231">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="c9425-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_203.png