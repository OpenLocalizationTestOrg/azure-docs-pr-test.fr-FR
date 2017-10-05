---
title: "Tutoriel : Intégration d’Azure Active Directory à Menlo Security | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Menlo Security."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9e63fe6b-0ad0-405d-9e41-6a1a40a41df8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: jeedes
ms.openlocfilehash: 75366abafa551d21630b0edddb65db23b9ea9d42
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-menlo-security"></a><span data-ttu-id="9eb04-103">Tutoriel : Intégration d’Azure Active Directory à Menlo Security</span><span class="sxs-lookup"><span data-stu-id="9eb04-103">Tutorial: Azure Active Directory integration with Menlo Security</span></span>

<span data-ttu-id="9eb04-104">Dans ce tutoriel, vous allez apprendre à intégrer Menlo Security à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9eb04-104">In this tutorial, you learn how to integrate Menlo Security with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9eb04-105">L’intégration de Menlo Security à Azure AD vous fait bénéficier des avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="9eb04-105">Integrating Menlo Security with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9eb04-106">Dans Azure AD, vous pouvez contrôler qui a accès à Menlo Security</span><span class="sxs-lookup"><span data-stu-id="9eb04-106">You can control in Azure AD who has access to Menlo Security</span></span>
- <span data-ttu-id="9eb04-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Menlo Security (via l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="9eb04-107">You can enable your users to automatically get signed-on to Menlo Security (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9eb04-108">Vous pouvez gérer vos comptes depuis un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="9eb04-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9eb04-109">Pour en savoir plus sur l’intégration de l’application SaaS avec Azure AD, consultez</span><span class="sxs-lookup"><span data-stu-id="9eb04-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="9eb04-110">[Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9eb04-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9eb04-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="9eb04-111">Prerequisites</span></span>

<span data-ttu-id="9eb04-112">Pour configurer l’intégration d’Azure AD avec Melo Security, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="9eb04-112">To configure Azure AD integration with Menlo Security, you need the following items:</span></span>

- <span data-ttu-id="9eb04-113">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="9eb04-113">An Azure AD subscription</span></span>
- <span data-ttu-id="9eb04-114">Un abonnement Menlo Security pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="9eb04-114">A Menlo Security single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9eb04-115">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="9eb04-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9eb04-116">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="9eb04-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9eb04-117">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="9eb04-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9eb04-118">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9eb04-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9eb04-119">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="9eb04-119">Scenario description</span></span>
<span data-ttu-id="9eb04-120">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="9eb04-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9eb04-121">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="9eb04-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9eb04-122">Ajout de Menlo Security à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="9eb04-122">Adding Menlo Security from the gallery</span></span>
2. <span data-ttu-id="9eb04-123">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9eb04-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-menlo-security-from-the-gallery"></a><span data-ttu-id="9eb04-124">Ajout de Menlo Security à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="9eb04-124">Adding Menlo Security from the gallery</span></span>
<span data-ttu-id="9eb04-125">Pour configurer l’intégration de Menlo Security à Azure AD, vous devez ajouter Menlo Security à votre liste d’applications SaaS gérées à partir de la galerie.</span><span class="sxs-lookup"><span data-stu-id="9eb04-125">To configure the integration of Menlo Security into Azure AD, you need to add Menlo Security from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9eb04-126">**Pour ajouter Menlo Security à partir de la galerie, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="9eb04-126">**To add Menlo Security from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9eb04-127">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9eb04-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9eb04-129">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="9eb04-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9eb04-130">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="9eb04-130">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="9eb04-132">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="9eb04-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="9eb04-134">Dans la zone de recherche, tapez **Menlo Security**.</span><span class="sxs-lookup"><span data-stu-id="9eb04-134">In the search box, type **Menlo Security**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_search.png)

5. <span data-ttu-id="9eb04-136">Dans le volet des résultats, sélectionnez **Menlo Security**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="9eb04-136">In the results panel, select **Menlo Security**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9eb04-138">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9eb04-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9eb04-139">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Menlo Security, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="9eb04-139">In this section, you configure and test Azure AD single sign-on with Menlo Security based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9eb04-140">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Menlo Security équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9eb04-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Menlo Security is to a user in Azure AD.</span></span> <span data-ttu-id="9eb04-141">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Menlo Security associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="9eb04-141">In other words, a link relationship between an Azure AD user and the related user in Menlo Security needs to be established.</span></span>

<span data-ttu-id="9eb04-142">Pour cela, affectez la valeur du champ **nom d’utilisateur** d’Azure AD comme valeur du champ **Username** de Menlo Security.</span><span class="sxs-lookup"><span data-stu-id="9eb04-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Menlo Security.</span></span>

<span data-ttu-id="9eb04-143">Pour configurer et tester l’authentification unique Azure AD avec Menlo Security, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="9eb04-143">To configure and test Azure AD single sign-on with Menlo Security, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9eb04-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="9eb04-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9eb04-145">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l'authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9eb04-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9eb04-146">**[Création d’un utilisateur de test Menlo Security](#creating-a-menlo-security-test-user)** pour avoir un équivalent de Britta Simon dans Menlo Security lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9eb04-146">**[Creating a Menlo Security test user](#creating-a-menlo-security-test-user)** - to have a counterpart of Britta Simon in Menlo Security that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9eb04-147">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d'utiliser l'authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9eb04-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9eb04-148">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="9eb04-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9eb04-149">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9eb04-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9eb04-150">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Menlo Security.</span><span class="sxs-lookup"><span data-stu-id="9eb04-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Menlo Security application.</span></span>

<span data-ttu-id="9eb04-151">**Pour configurer l’authentification unique Azure AD avec Menlo Security, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="9eb04-151">**To configure Azure AD single sign-on with Menlo Security, perform the following steps:**</span></span>

1. <span data-ttu-id="9eb04-152">Dans le portail Azure, dans la page d’intégration de l’application **Menlo Security**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="9eb04-152">In the Azure portal, on the **Menlo Security** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="9eb04-154">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="9eb04-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_samlbase.png)

3. <span data-ttu-id="9eb04-156">Dans la section **Domaine et URL Menlo Security**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="9eb04-156">On the **Menlo Security Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_url.png)

    <span data-ttu-id="9eb04-158">a.</span><span class="sxs-lookup"><span data-stu-id="9eb04-158">a.</span></span> <span data-ttu-id="9eb04-159">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<subdomain>.menlosecurity.com/account/login`</span><span class="sxs-lookup"><span data-stu-id="9eb04-159">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.menlosecurity.com/account/login`</span></span>

    <span data-ttu-id="9eb04-160">b.</span><span class="sxs-lookup"><span data-stu-id="9eb04-160">b.</span></span> <span data-ttu-id="9eb04-161">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<subdomain>.menlosecurity.com/safeview-auth-server/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="9eb04-161">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.menlosecurity.com/safeview-auth-server/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9eb04-162">Il ne s’agit pas des valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="9eb04-162">These values are not the real.</span></span> <span data-ttu-id="9eb04-163">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="9eb04-163">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="9eb04-164">Pour obtenir ces valeurs, contactez l’[équipe de support technique Menlo Security](https://www.menlosecurity.com/menlo-contact).</span><span class="sxs-lookup"><span data-stu-id="9eb04-164">Contact [Menlo Security Client support team](https://www.menlosecurity.com/menlo-contact) to get these values.</span></span> 
 
4. <span data-ttu-id="9eb04-165">Dans la section **Certificat de signature SAML**, cliquez sur **Certificat (en base64)**, puis enregistrez le fichier de certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="9eb04-165">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the Certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_certificate.png) 

5. <span data-ttu-id="9eb04-167">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="9eb04-167">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9eb04-169">Dans la section **Configuration de Menlo Security**, cliquez sur **Configurer Menlo Security** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="9eb04-169">On the **Menlo Security Configuration** section, click **Configure Menlo Security** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9eb04-170">Copiez l’**ID d’entité SAML** et l’**URL du service d’authentification unique SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="9eb04-170">Copy the **SAML Entity ID**, and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_configure.png) 

7. <span data-ttu-id="9eb04-172">Pour configurer l’authentification unique du côté de **Menlo Security**, connectez-vous au site web **Menlo Security** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="9eb04-172">To configure single sign-on on **Menlo Security** side, login to the **Menlo Security** website as an administrator.</span></span>

8. <span data-ttu-id="9eb04-173">Sous **Settings**, accédez à **Authentication** et effectuez les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="9eb04-173">Under **Settings** go to **Authentication** and perform following actions:</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-menlosecurity-tutorial/menlo_user_setup.png)

    <span data-ttu-id="9eb04-175">a.</span><span class="sxs-lookup"><span data-stu-id="9eb04-175">a.</span></span> <span data-ttu-id="9eb04-176">Cochez la case **Enable user authentication using SAML**.</span><span class="sxs-lookup"><span data-stu-id="9eb04-176">Tick the checkbox **Enable user authentication using SAML**.</span></span>

    <span data-ttu-id="9eb04-177">b.</span><span class="sxs-lookup"><span data-stu-id="9eb04-177">b.</span></span> <span data-ttu-id="9eb04-178">Définissez **Allow External Access** sur **Yes**.</span><span class="sxs-lookup"><span data-stu-id="9eb04-178">Select **Allow External Access** to **Yes**.</span></span>

    <span data-ttu-id="9eb04-179">c.</span><span class="sxs-lookup"><span data-stu-id="9eb04-179">c.</span></span> <span data-ttu-id="9eb04-180">Sous **SAML Provider**, sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9eb04-180">Under **SAML Provider**, select **Azure Active Directory**.</span></span>

    <span data-ttu-id="9eb04-181">d.</span><span class="sxs-lookup"><span data-stu-id="9eb04-181">d.</span></span> <span data-ttu-id="9eb04-182">**SAML 2.0 Endpoint** : collez l’**URL du service d’authentification unique SAML** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="9eb04-182">**SAML 2.0 Endpoint** : Paste the **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="9eb04-183">e.</span><span class="sxs-lookup"><span data-stu-id="9eb04-183">e.</span></span> <span data-ttu-id="9eb04-184">**Service Identifier (Issuer)** : collez l’**ID d’entité SAML** que vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="9eb04-184">**Service Identifier (Issuer)** : Paste the **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="9eb04-185">f.</span><span class="sxs-lookup"><span data-stu-id="9eb04-185">f.</span></span> <span data-ttu-id="9eb04-186">**X.509 Certificate** : ouvrez le **certificat (en base64)** téléchargé à partir du portail Azure dans le Bloc-notes et copiez-le dans cette zone.</span><span class="sxs-lookup"><span data-stu-id="9eb04-186">**X.509 Certificate** : Open the **Certificate (Base64)** downloaded from the Azure Portal in notepad and paste it in this box.</span></span>

    <span data-ttu-id="9eb04-187">g.</span><span class="sxs-lookup"><span data-stu-id="9eb04-187">g.</span></span> <span data-ttu-id="9eb04-188">Cliquez sur **Enregistrer** pour enregistrer les paramètres.</span><span class="sxs-lookup"><span data-stu-id="9eb04-188">Click **Save** to save the settings.</span></span>

> [!TIP]
> <span data-ttu-id="9eb04-189">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="9eb04-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9eb04-190">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="9eb04-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9eb04-191">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9eb04-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9eb04-192">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="9eb04-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="9eb04-193">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="9eb04-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="9eb04-195">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9eb04-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9eb04-196">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9eb04-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9eb04-198">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="9eb04-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9eb04-200">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="9eb04-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9eb04-202">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="9eb04-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9eb04-204">a.</span><span class="sxs-lookup"><span data-stu-id="9eb04-204">a.</span></span> <span data-ttu-id="9eb04-205">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9eb04-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9eb04-206">b.</span><span class="sxs-lookup"><span data-stu-id="9eb04-206">b.</span></span> <span data-ttu-id="9eb04-207">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9eb04-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9eb04-208">c.</span><span class="sxs-lookup"><span data-stu-id="9eb04-208">c.</span></span> <span data-ttu-id="9eb04-209">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="9eb04-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9eb04-210">d.</span><span class="sxs-lookup"><span data-stu-id="9eb04-210">d.</span></span> <span data-ttu-id="9eb04-211">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="9eb04-211">Click **Create**.</span></span>
 
### <a name="creating-a-menlo-security-test-user"></a><span data-ttu-id="9eb04-212">Création d’un utilisateur de test Menlo Security</span><span class="sxs-lookup"><span data-stu-id="9eb04-212">Creating a Menlo Security test user</span></span>
 
<span data-ttu-id="9eb04-213">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Menlo Security.</span><span class="sxs-lookup"><span data-stu-id="9eb04-213">In this section, you create a user called Britta Simon in Menlo Security.</span></span> <span data-ttu-id="9eb04-214">Rapprochez-vous de l’[équipe de support technique Menlo Security](https://www.menlosecurity.com/menlo-contact) pour ajouter les utilisateurs dans la plateforme Menlo Security.</span><span class="sxs-lookup"><span data-stu-id="9eb04-214">Work with [Menlo Security Client support team](https://www.menlosecurity.com/menlo-contact) to add the users in the Menlo Security platform.</span></span> <span data-ttu-id="9eb04-215">Les utilisateurs doivent être créés et activés avant que vous utilisiez l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="9eb04-215">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9eb04-216">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="9eb04-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9eb04-217">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Menlo Security.</span><span class="sxs-lookup"><span data-stu-id="9eb04-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Menlo Security.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="9eb04-219">**Pour affecter Britta Simon à Menlo Security, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="9eb04-219">**To assign Britta Simon to Menlo Security, perform the following steps:**</span></span>

1. <span data-ttu-id="9eb04-220">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="9eb04-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="9eb04-222">Dans la liste d’applications, sélectionnez **Menlo Security**.</span><span class="sxs-lookup"><span data-stu-id="9eb04-222">In the applications list, select **Menlo Security**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_app.png) 

3. <span data-ttu-id="9eb04-224">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="9eb04-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="9eb04-226">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="9eb04-226">Click **Add** button.</span></span> <span data-ttu-id="9eb04-227">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="9eb04-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="9eb04-229">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="9eb04-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9eb04-230">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="9eb04-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9eb04-231">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="9eb04-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9eb04-232">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="9eb04-232">Testing single sign-on</span></span>

<span data-ttu-id="9eb04-233">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9eb04-233">In this section, you test your Azure AD single sign-on configuration.</span></span>

<span data-ttu-id="9eb04-234">Ouvrez une fenêtre de navigateur en mode « InPrivate » ou « Incognito » afin de déclencher une nouvelle authentification.</span><span class="sxs-lookup"><span data-stu-id="9eb04-234">Open a browser window in an "InPrivate" or "Incognito" mode to trigger a new authentication.</span></span>  <span data-ttu-id="9eb04-235">Dans Internet Explorer, utilisez Ctrl+Maj+P.</span><span class="sxs-lookup"><span data-stu-id="9eb04-235">In Internet Explorer, use Ctrl+Shift+P.</span></span>  <span data-ttu-id="9eb04-236">Dans Chrome, utilisez Ctrl+Maj+N.</span><span class="sxs-lookup"><span data-stu-id="9eb04-236">In Chrome, use Ctrl+Shift+N.</span></span>  <span data-ttu-id="9eb04-237">Dans la fenêtre de navigation privée, accédez à une ressource protégée et connectez-vous à l’aide de vos identifiants Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9eb04-237">In the private browsing window, browse to a protected resource and perform an Azure AD login.</span></span>  <span data-ttu-id="9eb04-238">Dès la connexion établie, vous êtes redirigé vers le site demandé dans une session d’isolation.</span><span class="sxs-lookup"><span data-stu-id="9eb04-238">Upon successful login, you will be taken to the requested site in an isolation session.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9eb04-239">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="9eb04-239">Additional resources</span></span>

* [<span data-ttu-id="9eb04-240">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9eb04-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9eb04-241">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="9eb04-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_203.png

