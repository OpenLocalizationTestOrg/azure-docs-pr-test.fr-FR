---
title: "Didacticiel : intégration d’Azure Active Directory avec Kintone | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Kintone."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2b947dc-e1a8-4f5f-b40e-2c5180648e4f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: e5e847c12cba3611ce7ea2c3e956dbd55b1e0cac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kintone"></a><span data-ttu-id="8a5a3-103">Didacticiel : intégration d’Azure Active Directory avec Kintone</span><span class="sxs-lookup"><span data-stu-id="8a5a3-103">Tutorial: Azure Active Directory integration with Kintone</span></span>

<span data-ttu-id="8a5a3-104">L’objectif de ce didacticiel est de vous apprendre à intégrer Kintone avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8a5a3-104">In this tutorial, you learn how to integrate Kintone with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8a5a3-105">Intégrer Kintone avec Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="8a5a3-105">Integrating Kintone with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8a5a3-106">Dans Azure AD, vous pouvez contrôler l’accès à Kintone</span><span class="sxs-lookup"><span data-stu-id="8a5a3-106">You can control in Azure AD who has access to Kintone</span></span>
- <span data-ttu-id="8a5a3-107">Vous pouvez autoriser la connexion automatique à Kintone (via l’authentification unique) pour vos utilisateurs avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a5a3-107">You can enable your users to automatically get signed-on to Kintone (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8a5a3-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="8a5a3-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8a5a3-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8a5a3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8a5a3-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8a5a3-110">Prerequisites</span></span>

<span data-ttu-id="8a5a3-111">Pour configurer l’intégration d’Azure AD avec Kintone, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="8a5a3-111">To configure Azure AD integration with Kintone, you need the following items:</span></span>

- <span data-ttu-id="8a5a3-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a5a3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8a5a3-113">Un abonnement Kintone pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="8a5a3-113">A Kintone single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8a5a3-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8a5a3-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="8a5a3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8a5a3-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8a5a3-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8a5a3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8a5a3-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="8a5a3-118">Scenario description</span></span>
<span data-ttu-id="8a5a3-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8a5a3-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="8a5a3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8a5a3-121">Ajout de Kintone à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="8a5a3-121">Adding Kintone from the gallery</span></span>
2. <span data-ttu-id="8a5a3-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a5a3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kintone-from-the-gallery"></a><span data-ttu-id="8a5a3-123">Ajout de Kintone à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="8a5a3-123">Adding Kintone from the gallery</span></span>
<span data-ttu-id="8a5a3-124">Pour configurer l’intégration de Kintone avec Azure AD, vous devez ajouter Kintone, disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-124">To configure the integration of Kintone into Azure AD, you need to add Kintone from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8a5a3-125">**Pour ajouter Kintone à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8a5a3-125">**To add Kintone from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8a5a3-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8a5a3-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8a5a3-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="8a5a3-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="8a5a3-133">Dans la zone de recherche, entrez **Kintone**.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-133">In the search box, type **Kintone**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_search.png)

5. <span data-ttu-id="8a5a3-135">Dans le panneau de résultats, sélectionnez **Kintone**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-135">In the results panel, select **Kintone**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8a5a3-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a5a3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8a5a3-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Kintone, grâce à un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="8a5a3-138">In this section, you configure and test Azure AD single sign-on with Kintone based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8a5a3-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Kintone correspondant dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kintone is to a user in Azure AD.</span></span> <span data-ttu-id="8a5a3-140">En d’autres termes, il faut établir une relation entre l’utilisateur Azure AD et l’utilisateur Kintone associé.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-140">In other words, a link relationship between an Azure AD user and the related user in Kintone needs to be established.</span></span>

<span data-ttu-id="8a5a3-141">Dans Kintone, assigner la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **Nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-141">In Kintone, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8a5a3-142">Pour configurer et tester l’authentification unique Azure AD avec Kintone, vous devez compléter les blocs de construction suivants :</span><span class="sxs-lookup"><span data-stu-id="8a5a3-142">To configure and test Azure AD single sign-on with Kintone, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8a5a3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8a5a3-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8a5a3-145">**[Création d’un utilisateur de test Kintone](#creating-a-kintone-test-user)** pour avoir un équivalent de Britta Simon dans Kintone lié à la représentation d’un utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-145">**[Creating a Kintone test user](#creating-a-kintone-test-user)** - to have a counterpart of Britta Simon in Kintone that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8a5a3-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8a5a3-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8a5a3-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a5a3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8a5a3-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Kintone.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kintone application.</span></span>

<span data-ttu-id="8a5a3-150">**Pour configurer l’authentification unique Azure AD avec Kintone, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8a5a3-150">**To configure Azure AD single sign-on with Kintone, perform the following steps:**</span></span>

1. <span data-ttu-id="8a5a3-151">Dans le portail Azure, sur la page d’intégration de l’application **Kintone**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-151">In the Azure portal, on the **Kintone** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="8a5a3-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_samlbase.png)

3. <span data-ttu-id="8a5a3-155">Dans la section **Domaine et URL Kintone**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="8a5a3-155">On the **Kintone Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_url.png)

    <span data-ttu-id="8a5a3-157">a.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-157">a.</span></span> <span data-ttu-id="8a5a3-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<companyname>.kintone.com`</span><span class="sxs-lookup"><span data-stu-id="8a5a3-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.kintone.com`</span></span>

    <span data-ttu-id="8a5a3-159">b.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-159">b.</span></span> <span data-ttu-id="8a5a3-160">Dans la zone de texte **Identificateur**, entrez une URL au format suivant :</span><span class="sxs-lookup"><span data-stu-id="8a5a3-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.cybozu.com`|
    | `https://<companyname>.kintone.com`|

    > [!NOTE] 
    > <span data-ttu-id="8a5a3-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-161">These values are not real.</span></span> <span data-ttu-id="8a5a3-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8a5a3-163">Pour obtenir ces valeurs, contactez [l’équipe de support technique Kintone](https://www.kintone.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="8a5a3-163">Contact [Kintone Client support team](https://www.kintone.com/contact/) to get these values.</span></span> 
 
4. <span data-ttu-id="8a5a3-164">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_certificate.png) 

5. <span data-ttu-id="8a5a3-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="8a5a3-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kintone-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8a5a3-168">Pour ouvrir la fenêtre **Configurer l’authentification**, dans la section **Configuration Kintone**, cliquez sur **Configurer Kintone**.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-168">On the **Kintone Configuration** section, click **Configure Kintone** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8a5a3-169">Copiez **l’URL de déconnexion et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_configure.png) 

7. <span data-ttu-id="8a5a3-171">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise **Kintone** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-171">In a different web browser window, log into your **Kintone** company site as an administrator.</span></span>

8. <span data-ttu-id="8a5a3-172">Cliquez sur **Settings**.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-172">Click **Settings**.</span></span>
   
    <span data-ttu-id="8a5a3-173">![Paramètres](./media/active-directory-saas-kintone-tutorial/ic785879.png "Paramètres")</span><span class="sxs-lookup"><span data-stu-id="8a5a3-173">![Settings](./media/active-directory-saas-kintone-tutorial/ic785879.png "Settings")</span></span>

9. <span data-ttu-id="8a5a3-174">Cliquez sur **Users & System Administration**.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-174">Click **Users & System Administration**.</span></span>
   
    <span data-ttu-id="8a5a3-175">![Administration système et utilisateurs](./media/active-directory-saas-kintone-tutorial/ic785880.png "Administration système et utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="8a5a3-175">![Users & System Administration](./media/active-directory-saas-kintone-tutorial/ic785880.png "Users & System Administration")</span></span>

10. <span data-ttu-id="8a5a3-176">Sous **System Administration \> Security**, cliquez sur **Login**.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-176">Under **System Administration \> Security** click **Login**.</span></span>
   
    <span data-ttu-id="8a5a3-177">![Connexion](./media/active-directory-saas-kintone-tutorial/ic785881.png "Connexion")</span><span class="sxs-lookup"><span data-stu-id="8a5a3-177">![Login](./media/active-directory-saas-kintone-tutorial/ic785881.png "Login")</span></span>

11. <span data-ttu-id="8a5a3-178">Cliquez sur **Enable SAML authentication**.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-178">Click **Enable SAML authentication**.</span></span>
   
    <span data-ttu-id="8a5a3-179">![Authentification SAML](./media/active-directory-saas-kintone-tutorial/ic785882.png "Authentification SAML")</span><span class="sxs-lookup"><span data-stu-id="8a5a3-179">![SAML Authentication](./media/active-directory-saas-kintone-tutorial/ic785882.png "SAML Authentication")</span></span>

12. <span data-ttu-id="8a5a3-180">Dans la section SAML Authentication, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="8a5a3-180">In the SAML Authentication section, perform the following steps:</span></span>
    
    <span data-ttu-id="8a5a3-181">![Authentification SAML](./media/active-directory-saas-kintone-tutorial/ic785883.png "Authentification SAML")</span><span class="sxs-lookup"><span data-stu-id="8a5a3-181">![SAML Authentication](./media/active-directory-saas-kintone-tutorial/ic785883.png "SAML Authentication")</span></span>
    
    <span data-ttu-id="8a5a3-182">a.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-182">a.</span></span> <span data-ttu-id="8a5a3-183">Dans la zone de texte **URL de connexion**, collez la valeur de l’**URL du service d’authentification unique SAML** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-183">In the **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="8a5a3-184">b.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-184">b.</span></span> <span data-ttu-id="8a5a3-185">Dans la zone de texte **URL de déconnexion**, collez la valeur de l’**URL de déconnexion** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-185">In the **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="8a5a3-186">c.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-186">c.</span></span> <span data-ttu-id="8a5a3-187">Cliquez sur **Parcourir** pour charger le certificat téléchargé.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-187">Click **Browse** to upload your downloaded certificate.</span></span>
    
    <span data-ttu-id="8a5a3-188">d.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-188">d.</span></span> <span data-ttu-id="8a5a3-189">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-189">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="8a5a3-190">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8a5a3-191">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8a5a3-192">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8a5a3-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8a5a3-193">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a5a3-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="8a5a3-194">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="8a5a3-196">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8a5a3-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8a5a3-197">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kintone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8a5a3-199">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kintone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8a5a3-201">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kintone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8a5a3-203">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="8a5a3-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kintone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8a5a3-205">a.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-205">a.</span></span> <span data-ttu-id="8a5a3-206">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8a5a3-207">b.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-207">b.</span></span> <span data-ttu-id="8a5a3-208">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8a5a3-209">c.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-209">c.</span></span> <span data-ttu-id="8a5a3-210">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8a5a3-211">d.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-211">d.</span></span> <span data-ttu-id="8a5a3-212">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-212">Click **Create**.</span></span>
 
### <a name="creating-a-kintone-test-user"></a><span data-ttu-id="8a5a3-213">Création d’un utilisateur de test Kintone</span><span class="sxs-lookup"><span data-stu-id="8a5a3-213">Creating a Kintone test user</span></span>

<span data-ttu-id="8a5a3-214">Pour que les utilisateurs Azure AD puissent se connecter à Kintone, ils doivent être approvisionnés dans Kintone.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-214">To enable Azure AD users to log in to Kintone, they must be provisioned into Kintone.</span></span>  
<span data-ttu-id="8a5a3-215">Dans le cas de Kintone, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-215">In the case of Kintone, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="8a5a3-216">Pour approvisionner un compte d’utilisateur, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="8a5a3-216">To provision a user account, perform the following steps:</span></span>

1. <span data-ttu-id="8a5a3-217">Connectez-vous à votre site d’entreprise **Kintone** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-217">Log in to your **Kintone** company site as an administrator.</span></span>

2. <span data-ttu-id="8a5a3-218">Cliquez sur **Setting**.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-218">Click **Setting**.</span></span>
   
    <span data-ttu-id="8a5a3-219">![Paramètres](./media/active-directory-saas-kintone-tutorial/ic785879.png "Paramètres")</span><span class="sxs-lookup"><span data-stu-id="8a5a3-219">![Settings](./media/active-directory-saas-kintone-tutorial/ic785879.png "Settings")</span></span>

3. <span data-ttu-id="8a5a3-220">Cliquez sur **Users & System Administration**.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-220">Click **Users & System Administration**.</span></span>
   
    <span data-ttu-id="8a5a3-221">![Administration système et utilisateur](./media/active-directory-saas-kintone-tutorial/ic785880.png "Administration système et utilisateur")</span><span class="sxs-lookup"><span data-stu-id="8a5a3-221">![User & System Administration](./media/active-directory-saas-kintone-tutorial/ic785880.png "User & System Administration")</span></span>

4. <span data-ttu-id="8a5a3-222">Sous **User Administration**, cliquez sur **Departments & Users**.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-222">Under **User Administration**, click **Departments & Users**.</span></span>
   
    <span data-ttu-id="8a5a3-223">![Département et utilisateurs](./media/active-directory-saas-kintone-tutorial/ic785888.png "Département et utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="8a5a3-223">![Department & Users](./media/active-directory-saas-kintone-tutorial/ic785888.png "Department & Users")</span></span>

5. <span data-ttu-id="8a5a3-224">Cliquez sur **New User**.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-224">Click **New User**.</span></span>
   
    <span data-ttu-id="8a5a3-225">![Nouveaux utilisateurs](./media/active-directory-saas-kintone-tutorial/ic785889.png "Nouveaux utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="8a5a3-225">![New Users](./media/active-directory-saas-kintone-tutorial/ic785889.png "New Users")</span></span>

6. <span data-ttu-id="8a5a3-226">Dans la section **New User**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="8a5a3-226">In the **New User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="8a5a3-227">![Nouveaux utilisateurs](./media/active-directory-saas-kintone-tutorial/ic785890.png "Nouveaux utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="8a5a3-227">![New Users](./media/active-directory-saas-kintone-tutorial/ic785890.png "New Users")</span></span>
   
    <span data-ttu-id="8a5a3-228">a.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-228">a.</span></span> <span data-ttu-id="8a5a3-229">Dans les zones de texte correspondantes, entrez un **Nom d’affichage**, un **Nom de connexion**, un **Nouveau mot de passe**, confirmez-le dans **Confirmer le mot de passe**, entrez ainsi une **adresse e-mail** et d’autres détails d’un compte AAD valide à provisionner.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-229">Type a **Display Name**, **Login Name**, **New Password**, **Confirm Password**, **E-mail Address**, and other details of a valid AAD account you want to provision into the related textboxes.</span></span>
 
    <span data-ttu-id="8a5a3-230">b.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-230">b.</span></span> <span data-ttu-id="8a5a3-231">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-231">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="8a5a3-232">Vous pouvez utiliser n’importe quel autre outil ou API de création de compte d’utilisateur Kintone fourni par ce service pour approvisionner des comptes d’utilisateurs Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-232">You can use any other Kintone user account creation tools or APIs provided by Kintone to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8a5a3-233">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="8a5a3-233">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8a5a3-234">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant un accès à Kintone.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-234">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kintone.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="8a5a3-236">**Pour assigner Britta Simon à Kintone, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="8a5a3-236">**To assign Britta Simon to Kintone, perform the following steps:**</span></span>

1. <span data-ttu-id="8a5a3-237">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-237">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="8a5a3-239">Dans la liste des applications, sélectionnez **Kintone**.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-239">In the applications list, select **Kintone**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kintone-tutorial/tutorial_kintone_app.png) 

3. <span data-ttu-id="8a5a3-241">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-241">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="8a5a3-243">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-243">Click **Add** button.</span></span> <span data-ttu-id="8a5a3-244">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="8a5a3-246">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8a5a3-247">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8a5a3-248">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8a5a3-249">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="8a5a3-249">Testing single sign-on</span></span>

<span data-ttu-id="8a5a3-250">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-250">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8a5a3-251">En cliquant sur la vignette Kintone dans le Panneau d’accès, vous allez en principe être connecté automatiquement à votre application Kintone.</span><span class="sxs-lookup"><span data-stu-id="8a5a3-251">When you click the Kintone tile in the Access Panel, you should get automatically signed-on to your Kintone application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8a5a3-252">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="8a5a3-252">Additional resources</span></span>

* [<span data-ttu-id="8a5a3-253">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8a5a3-253">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8a5a3-254">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="8a5a3-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kintone-tutorial/tutorial_general_203.png

