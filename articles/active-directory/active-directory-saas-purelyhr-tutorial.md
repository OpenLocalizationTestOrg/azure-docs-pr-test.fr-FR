---
title: "Didacticiel : Intégration d’Azure Active Directory avec PurelyHR | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et PurelyHR."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 86a9c454-596d-4902-829a-fe126708f739
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: jeedes
ms.openlocfilehash: a9075b1759ebd39f164bfe288fb0a365acdcc44c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-purelyhr"></a><span data-ttu-id="8594f-103">Didacticiel : Intégration d’Azure Active Directory avec PurelyHR</span><span class="sxs-lookup"><span data-stu-id="8594f-103">Tutorial: Azure Active Directory integration with PurelyHR</span></span>

<span data-ttu-id="8594f-104">Dans ce didacticiel, vous allez apprendre à intégrer PurelyHR avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8594f-104">In this tutorial, you learn how to integrate PurelyHR with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8594f-105">L’intégration de PurelyHR avec Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="8594f-105">Integrating PurelyHR with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8594f-106">Dans Azure AD, vous pouvez contrôler qui a accès à PurelyHR</span><span class="sxs-lookup"><span data-stu-id="8594f-106">You can control in Azure AD who has access to PurelyHR</span></span>
- <span data-ttu-id="8594f-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à PurelyHR (par le biais de l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="8594f-107">You can enable your users to automatically get signed-on to PurelyHR (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8594f-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="8594f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8594f-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8594f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8594f-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8594f-110">Prerequisites</span></span>

<span data-ttu-id="8594f-111">Pour configurer l’intégration d’Azure AD avec PurelyHR, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="8594f-111">To configure Azure AD integration with PurelyHR, you need the following items:</span></span>

- <span data-ttu-id="8594f-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="8594f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8594f-113">Un abonnement PurelyHR pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="8594f-113">A PurelyHR single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8594f-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="8594f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8594f-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="8594f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8594f-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="8594f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8594f-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8594f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8594f-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="8594f-118">Scenario description</span></span>
<span data-ttu-id="8594f-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="8594f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8594f-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="8594f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8594f-121">Ajout de PurelyHR à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="8594f-121">Adding PurelyHR from the gallery</span></span>
2. <span data-ttu-id="8594f-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8594f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-purelyhr-from-the-gallery"></a><span data-ttu-id="8594f-123">Ajout de PurelyHR à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="8594f-123">Adding PurelyHR from the gallery</span></span>
<span data-ttu-id="8594f-124">Pour configurer l’intégration de PurelyHR avec Azure AD, vous devez ajouter PurelyHR à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="8594f-124">To configure the integration of PurelyHR into Azure AD, you need to add PurelyHR from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8594f-125">**Pour ajouter PurelyHR à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8594f-125">**To add PurelyHR from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8594f-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8594f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8594f-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="8594f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8594f-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="8594f-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="8594f-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="8594f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="8594f-133">Dans le champ de recherche, tapez **PurelyHR**.</span><span class="sxs-lookup"><span data-stu-id="8594f-133">In the search box, type **PurelyHR**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_search.png)

5. <span data-ttu-id="8594f-135">Dans le volet de résultats, sélectionnez **PurelyHR**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="8594f-135">In the results panel, select **PurelyHR**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8594f-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8594f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8594f-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec PurelyHR, par le biais d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="8594f-138">In this section, you configure and test Azure AD single sign-on with PurelyHR based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8594f-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur PurelyHR correspondant dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8594f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in PurelyHR is to a user in Azure AD.</span></span> <span data-ttu-id="8594f-140">En d’autres termes, une relation entre un utilisateur Azure AD et l’utilisateur PurelyHR associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="8594f-140">In other words, a link relationship between an Azure AD user and the related user in PurelyHR needs to be established.</span></span>

<span data-ttu-id="8594f-141">Dans PurelyHR, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="8594f-141">In PurelyHR, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8594f-142">Pour configurer et tester l’authentification unique Azure AD avec PurelyHR, vous devez vous conformer aux indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="8594f-142">To configure and test Azure AD single sign-on with PurelyHR, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8594f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="8594f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8594f-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8594f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8594f-145">**[Création d’un utilisateur de test PurelyHR](#creating-a-purelyhr-test-user)** pour avoir un équivalent de Britta Simon dans PurelyHR lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8594f-145">**[Creating a PurelyHR test user](#creating-a-purelyhr-test-user)** - to have a counterpart of Britta Simon in PurelyHR that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8594f-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8594f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8594f-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="8594f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8594f-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8594f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8594f-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="8594f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your PurelyHR application.</span></span>

<span data-ttu-id="8594f-150">**Pour configurer l’authentification unique Azure AD avec PurelyHR, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8594f-150">**To configure Azure AD single sign-on with PurelyHR, perform the following steps:**</span></span>

1. <span data-ttu-id="8594f-151">Dans le portail Azure, sur la page d’intégration de l’application **PurelyHR**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="8594f-151">In the Azure portal, on the **PurelyHR** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="8594f-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="8594f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_samlbase.png)

3. <span data-ttu-id="8594f-155">Dans la section **Domaines et URL PurelyHR**, suivez les étapes ci-dessous si vous souhaitez configurer l’application en mode initié par **IDP** :</span><span class="sxs-lookup"><span data-stu-id="8594f-155">On the **PurelyHR Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_url.png)
   
    <span data-ttu-id="8594f-157">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://<companyID>.purelyhr.com/sso-consume`</span><span class="sxs-lookup"><span data-stu-id="8594f-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyID>.purelyhr.com/sso-consume`</span></span>

4. <span data-ttu-id="8594f-158">Cochez **Afficher les paramètres d’URL avancés** si vous souhaitez configurer l’application en mode lancé par le **fournisseur de service** :</span><span class="sxs-lookup"><span data-stu-id="8594f-158">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_url1.png)
    
    <span data-ttu-id="8594f-160">Dans la zone de texte **URL de connexion**, tapez la valeur au format suivant : `https://<companyID>.purelyhr.com/sso-initiate`</span><span class="sxs-lookup"><span data-stu-id="8594f-160">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<companyID>.purelyhr.com/sso-initiate`</span></span>
     
    > [!NOTE]
    > <span data-ttu-id="8594f-161">Il ne s’agit pas des valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="8594f-161">These values are not the real.</span></span> <span data-ttu-id="8594f-162">Mettez à jour ces valeurs avec l’URL de réponse et l’URL de connexion réelles.</span><span class="sxs-lookup"><span data-stu-id="8594f-162">Update these values with the actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="8594f-163">Pour obtenir ces valeurs, contactez l’[équipe de support technique PurelyHR](http://support.purelyhr.com/).</span><span class="sxs-lookup"><span data-stu-id="8594f-163">Contact [PurelyHR Client support team](http://support.purelyhr.com/) to get these values.</span></span> 

5. <span data-ttu-id="8594f-164">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="8594f-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_certificate.png) 

6. <span data-ttu-id="8594f-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="8594f-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-purelyhr-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="8594f-168">Dans la section **Configuration de PurelyHR**, cliquez sur **Configurer PurelyHR** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="8594f-168">On the **PurelyHR Configuration** section, click **Configure PurelyHR** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8594f-169">Copiez l’**ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="8594f-169">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_configure.png) 

8. <span data-ttu-id="8594f-171">Pour configurer l’authentification unique côté **PurelyHR**, connectez-vous au site web en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="8594f-171">To configure single sign-on on **PurelyHR** side, login to their website as an administrator.</span></span>

9. <span data-ttu-id="8594f-172">Ouvrez le **tableau de bord** dans la barre d’outils et cliquez sur **SSO Settings** (Paramètres d’authentification unique).</span><span class="sxs-lookup"><span data-stu-id="8594f-172">Open the **Dashboard** from the options in the toolbar and click **SSO Settings**.</span></span>

10. <span data-ttu-id="8594f-173">Collez les valeurs dans les zones comme décrit ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="8594f-173">Paste the values in the boxes as described below-</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-purelyhr-tutorial/purelyhr-dashboard-sso-settings.png)    

    <span data-ttu-id="8594f-175">a.</span><span class="sxs-lookup"><span data-stu-id="8594f-175">a.</span></span> <span data-ttu-id="8594f-176">Ouvrez le **Certificat (Base64)** téléchargé à partir du portail Azure dans le bloc-notes et copiez la valeur du certificat.</span><span class="sxs-lookup"><span data-stu-id="8594f-176">Open the **Certificate(Bas64)** downloaded from the Azure portal in notepad and copy the certificate value.</span></span> <span data-ttu-id="8594f-177">Collez la valeur copiée dans la zone **Certificat x509**.</span><span class="sxs-lookup"><span data-stu-id="8594f-177">Paste the copied value into the **X.509 Certificate** box.</span></span>

    <span data-ttu-id="8594f-178">b.</span><span class="sxs-lookup"><span data-stu-id="8594f-178">b.</span></span> <span data-ttu-id="8594f-179">Dans la zone **Idp Issuer URL** (URL d’émetteur IdP), collez l’**ID d’entité SAML** copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8594f-179">In the **Idp Issuer URL** box, paste the **SAML Entity ID** copied from the Azure portal.</span></span>

    <span data-ttu-id="8594f-180">c.</span><span class="sxs-lookup"><span data-stu-id="8594f-180">c.</span></span> <span data-ttu-id="8594f-181">Dans la zone **Idp Endpoint URL** (URL de point de terminaison IdP), collez l’**URL d’authentification unique SAML** copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8594f-181">In the **Idp Endpoint URL** box, paste the **SAML Single Sign-On Service URL** copied from the Azure portal.</span></span> 

    <span data-ttu-id="8594f-182">d.</span><span class="sxs-lookup"><span data-stu-id="8594f-182">d.</span></span> <span data-ttu-id="8594f-183">Cochez la case **Auto-Create Users** (Créer automatiquement des utilisateurs) pour activer l’approvisionnement automatique des utilisateurs dans PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="8594f-183">Check the **Auto-Create Users** checkbox to enable automatic user provisioning in PurelyHR.</span></span>

    <span data-ttu-id="8594f-184">e.</span><span class="sxs-lookup"><span data-stu-id="8594f-184">e.</span></span> <span data-ttu-id="8594f-185">Cliquez sur **Enregistrer les modifications** pour enregistrer les paramètres.</span><span class="sxs-lookup"><span data-stu-id="8594f-185">Click **Save Changes** to save the settings.</span></span>

> [!TIP]
> <span data-ttu-id="8594f-186">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="8594f-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8594f-187">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="8594f-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8594f-188">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8594f-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8594f-189">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="8594f-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="8594f-190">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8594f-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="8594f-192">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8594f-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8594f-193">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8594f-193">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8594f-195">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="8594f-195">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8594f-197">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="8594f-197">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8594f-199">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="8594f-199">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-purelyhr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8594f-201">a.</span><span class="sxs-lookup"><span data-stu-id="8594f-201">a.</span></span> <span data-ttu-id="8594f-202">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8594f-202">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8594f-203">b.</span><span class="sxs-lookup"><span data-stu-id="8594f-203">b.</span></span> <span data-ttu-id="8594f-204">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8594f-204">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8594f-205">c.</span><span class="sxs-lookup"><span data-stu-id="8594f-205">c.</span></span> <span data-ttu-id="8594f-206">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="8594f-206">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8594f-207">d.</span><span class="sxs-lookup"><span data-stu-id="8594f-207">d.</span></span> <span data-ttu-id="8594f-208">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="8594f-208">Click **Create**.</span></span>
 
### <a name="creating-a-purelyhr-test-user"></a><span data-ttu-id="8594f-209">Création d’un utilisateur de test PurelyHR</span><span class="sxs-lookup"><span data-stu-id="8594f-209">Creating a PurelyHR test user</span></span>

<span data-ttu-id="8594f-210">Pour se connecter à PurelyHR, les utilisateurs d’Azure AD doivent être approvisionnés dans PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="8594f-210">To enable Azure AD users to log in to PurelyHR, they must be provisioned into PurelyHR.</span></span> <span data-ttu-id="8594f-211">Dans PurelyHR, l’approvisionnement est une tâche automatique. Aucune opération manuelle n’est nécessaire lorsque l’approvisionnement automatique de l’utilisateur est activé.</span><span class="sxs-lookup"><span data-stu-id="8594f-211">In PurelyHR, provisioning is an automatic task and no manual steps are required when automatic user provisioning is enabled.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8594f-212">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="8594f-212">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8594f-213">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à PurelyHR.</span><span class="sxs-lookup"><span data-stu-id="8594f-213">In this section, you enable Britta Simon to use Azure single sign-on by granting access to PurelyHR.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="8594f-215">**Pour affecter Britta Simon à PurelyHR, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8594f-215">**To assign Britta Simon to PurelyHR, perform the following steps:**</span></span>

1. <span data-ttu-id="8594f-216">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="8594f-216">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="8594f-218">Dans la liste des applications, sélectionnez **PurelyHR**.</span><span class="sxs-lookup"><span data-stu-id="8594f-218">In the applications list, select **PurelyHR**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-purelyhr-tutorial/tutorial_purelyhr_app.png) 

3. <span data-ttu-id="8594f-220">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="8594f-220">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="8594f-222">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="8594f-222">Click **Add** button.</span></span> <span data-ttu-id="8594f-223">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="8594f-223">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="8594f-225">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="8594f-225">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8594f-226">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="8594f-226">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8594f-227">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="8594f-227">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8594f-228">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="8594f-228">Testing single sign-on</span></span>

<span data-ttu-id="8594f-229">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="8594f-229">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8594f-230">Lorsque vous cliquez sur la mosaïque Absorb LMS dans le volet d’accès, vous êtes automatiquement connecté à votre application Absorb LMS.</span><span class="sxs-lookup"><span data-stu-id="8594f-230">Click the Absorb LMS tile in the Access Panel, you get automatically signed-on to your Absorb LMS application.</span></span>

<span data-ttu-id="8594f-231">Pour plus d’informations sur le volet d’accès, consultez</span><span class="sxs-lookup"><span data-stu-id="8594f-231">For more information about the Access Panel, see.</span></span> <span data-ttu-id="8594f-232">[Présentation du volet d’accès](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="8594f-232">[Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8594f-233">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="8594f-233">Additional resources</span></span>

* [<span data-ttu-id="8594f-234">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8594f-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8594f-235">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="8594f-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-purelyhr-tutorial/tutorial_general_203.png

