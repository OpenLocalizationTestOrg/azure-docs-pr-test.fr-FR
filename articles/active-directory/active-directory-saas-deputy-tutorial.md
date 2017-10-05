---
title: "Didacticiel : intégration d’Azure Active Directory à Deputy | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Deputy."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5665c3ac-5689-4201-80fe-fcc677d4430d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 51aed908208b7a40ea2ab710dffe84370b573991
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-deputy"></a><span data-ttu-id="6be30-103">Didacticiel : Intégration d’Azure Active Directory avec Deputy</span><span class="sxs-lookup"><span data-stu-id="6be30-103">Tutorial: Azure Active Directory integration with Deputy</span></span>

<span data-ttu-id="6be30-104">Dans ce didacticiel, vous allez apprendre à intégrer Deputy à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6be30-104">In this tutorial, you learn how to integrate Deputy with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6be30-105">L’intégration de Deputy dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="6be30-105">Integrating Deputy with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6be30-106">Dans Azure AD, vous pouvez contrôler qui a accès à Deputy</span><span class="sxs-lookup"><span data-stu-id="6be30-106">You can control in Azure AD who has access to Deputy</span></span>
- <span data-ttu-id="6be30-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Deputy (via l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="6be30-107">You can enable your users to automatically get signed-on to Deputy (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6be30-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="6be30-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6be30-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6be30-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6be30-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="6be30-110">Prerequisites</span></span>

<span data-ttu-id="6be30-111">Pour configurer l’intégration d’Azure AD avec Deputy, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="6be30-111">To configure Azure AD integration with Deputy, you need the following items:</span></span>

- <span data-ttu-id="6be30-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="6be30-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6be30-113">Un abonnement Deputy pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="6be30-113">A Deputy single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6be30-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="6be30-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6be30-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="6be30-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6be30-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="6be30-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6be30-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6be30-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6be30-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="6be30-118">Scenario description</span></span>
<span data-ttu-id="6be30-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="6be30-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6be30-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="6be30-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6be30-121">Ajout de Deputy depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="6be30-121">Adding Deputy from the gallery</span></span>
2. <span data-ttu-id="6be30-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="6be30-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-deputy-from-the-gallery"></a><span data-ttu-id="6be30-123">Ajout de Deputy depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="6be30-123">Adding Deputy from the gallery</span></span>
<span data-ttu-id="6be30-124">Pour configurer l’intégration de Deputy avec Azure AD, vous devez ajouter Deputy, à partir de la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="6be30-124">To configure the integration of Deputy into Azure AD, you need to add Deputy from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6be30-125">**Pour ajouter Deputy à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6be30-125">**To add Deputy from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6be30-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6be30-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6be30-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="6be30-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6be30-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="6be30-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="6be30-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="6be30-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="6be30-133">Dans la zone de recherche, tapez **Deputy**.</span><span class="sxs-lookup"><span data-stu-id="6be30-133">In the search box, type **Deputy**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_search.png)

5. <span data-ttu-id="6be30-135">Dans le volet de résultats, sélectionnez **Deputy**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="6be30-135">In the results panel, select **Deputy**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6be30-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="6be30-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6be30-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Deputy, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="6be30-138">In this section, you configure and test Azure AD single sign-on with Deputy based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6be30-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Deputy correspondant dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6be30-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Deputy is to a user in Azure AD.</span></span> <span data-ttu-id="6be30-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Deputy associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="6be30-140">In other words, a link relationship between an Azure AD user and the related user in Deputy needs to be established.</span></span>

<span data-ttu-id="6be30-141">Dans Deputy, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="6be30-141">In Deputy, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6be30-142">Pour configurer et tester l’authentification unique Azure AD avec Deputy, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="6be30-142">To configure and test Azure AD single sign-on with Deputy, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6be30-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="6be30-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6be30-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6be30-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6be30-145">**[Création d’un utilisateur de test Deputy](#creating-a-deputy-test-user)** pour avoir un équivalent de Britta Simon dans Deputy lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="6be30-145">**[Creating a Deputy test user](#creating-a-deputy-test-user)** - to have a counterpart of Britta Simon in Deputy that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6be30-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6be30-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6be30-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="6be30-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6be30-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="6be30-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6be30-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Deputy.</span><span class="sxs-lookup"><span data-stu-id="6be30-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Deputy application.</span></span>

<span data-ttu-id="6be30-150">**Pour configurer l’authentification unique Azure AD avec Deputy, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6be30-150">**To configure Azure AD single sign-on with Deputy, perform the following steps:**</span></span>

1. <span data-ttu-id="6be30-151">Dans le portail Azure, sur la page d’intégration de l’application **Deputy**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="6be30-151">In the Azure portal, on the **Deputy** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="6be30-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="6be30-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_samlbase.png)

3. <span data-ttu-id="6be30-155">Dans la section **Domaine et URL Deputy**, si vous souhaitez configurer l’application en mode initié par **IDP**, suivez les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="6be30-155">On the **Deputy Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_url1.png)

    <span data-ttu-id="6be30-157">a.</span><span class="sxs-lookup"><span data-stu-id="6be30-157">a.</span></span> <span data-ttu-id="6be30-158">Dans la zone de texte **Identificateur**, tapez une URL au format suivant :</span><span class="sxs-lookup"><span data-stu-id="6be30-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    |  |
    | ----|
    | `https://<subdomain>.<region>.au.deputy.com` |
    | `https://<subdomain>.<region>.ent-au.deputy.com` |
    | `https://<subdomain>.<region>.na.deputy.com`|
    | `https://<subdomain>.<region>.ent-na.deputy.com`|
    | `https://<subdomain>.<region>.eu.deputy.com` |
    | `https://<subdomain>.<region>.ent-eu.deputy.com` |
    | `https://<subdomain>.<region>.as.deputy.com` |
    | `https://<subdomain>.<region>.ent-as.deputy.com` |
    | `https://<subdomain>.<region>.la.deputy.com` |
    | `https://<subdomain>.<region>.ent-la.deputy.com` |
    | `https://<subdomain>.<region>.af.deputy.com` |
    | `https://<subdomain>.<region>.ent-af.deputy.com` |
    | `https://<subdomain>.<region>.an.deputy.com` |
    | `https://<subdomain>.<region>.ent-an.deputy.com` |
    | `https://<subdomain>.<region>.deputy.com` |

    <span data-ttu-id="6be30-159">b.</span><span class="sxs-lookup"><span data-stu-id="6be30-159">b.</span></span> <span data-ttu-id="6be30-160">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant :</span><span class="sxs-lookup"><span data-stu-id="6be30-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |----|
    | `https://<subdomain>.<region>.au.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-au.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.na.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-na.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.eu.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-eu.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.as.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-as.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.la.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-la.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.af.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-af.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.an.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-an.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.deputy.com/exec/devapp/samlacs.` |

4. <span data-ttu-id="6be30-161">Cliquez sur **Afficher les paramètres d’URL avancés**.</span><span class="sxs-lookup"><span data-stu-id="6be30-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="6be30-162">Si vous souhaitez configurer l’application en mode initié par le **fournisseur de service** :</span><span class="sxs-lookup"><span data-stu-id="6be30-162">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_url2.png)

    <span data-ttu-id="6be30-164">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<your-subdomain>.<region>.deputy.com`</span><span class="sxs-lookup"><span data-stu-id="6be30-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<your-subdomain>.<region>.deputy.com`</span></span>
    
    >[!NOTE]
    > <span data-ttu-id="6be30-165">Le suffixe de région Deputy est facultatif ou il doit utiliser l’une des valeurs suivantes : au | na | eu |as |la |af |an |ent-au |ent-na |ent-eu |ent-as | ent-la | ent-af | ent-an</span><span class="sxs-lookup"><span data-stu-id="6be30-165">Deputy region suffix is optional, or it should use one of these: au | na | eu |as |la |af |an |ent-au |ent-na |ent-eu |ent-as | ent-la | ent-af | ent-an</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6be30-166">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="6be30-166">These values are not real.</span></span> <span data-ttu-id="6be30-167">Mettez à jour ces valeurs avec l’identificateur, l’URL de réponse et l’URL de connexion réels.</span><span class="sxs-lookup"><span data-stu-id="6be30-167">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="6be30-168">Pour obtenir ces valeurs, contactez [l’équipe de support technique de Deputy](https://www.deputy.com/call-centers-customer-support-scheduling-software).</span><span class="sxs-lookup"><span data-stu-id="6be30-168">Contact [Deputy support team](https://www.deputy.com/call-centers-customer-support-scheduling-software) to get these values.</span></span> 

5. <span data-ttu-id="6be30-169">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="6be30-169">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_certificate.png) 

6. <span data-ttu-id="6be30-171">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="6be30-171">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-deputy-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="6be30-173">Dans la section **Configuration de Deputy** , cliquez sur **Configurer Deputy** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="6be30-173">On the **Deputy Configuration** section, click **Configure Deputy** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6be30-174">Copiez l**’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="6be30-174">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_configure.png) 

8. <span data-ttu-id="6be30-176">Accédez à l’URL suivante :[https://(votre-sous-domaine).deputy.com/exec/config/system_config]( https://(your-subdomain).deputy.com/exec/config/system_config).</span><span class="sxs-lookup"><span data-stu-id="6be30-176">Navigate to the following URL:[https://(your-subdomain).deputy.com/exec/config/system_config]( https://(your-subdomain).deputy.com/exec/config/system_config).</span></span> <span data-ttu-id="6be30-177">Accédez aux **Paramètres de sécurité** et cliquez sur **Modifier**.</span><span class="sxs-lookup"><span data-stu-id="6be30-177">Go to **Security Settings** and click **Edit**.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_004.png)

9. <span data-ttu-id="6be30-179">Sur cette page **Paramètres de sécurité** , procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="6be30-179">On this **Security Settings** page, perform below steps.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_005.png)
    
    <span data-ttu-id="6be30-181">a.</span><span class="sxs-lookup"><span data-stu-id="6be30-181">a.</span></span> <span data-ttu-id="6be30-182">Activez la **connexion à partir de réseaux sociaux**.</span><span class="sxs-lookup"><span data-stu-id="6be30-182">Enable **Social Login**.</span></span>
   
    <span data-ttu-id="6be30-183">b.</span><span class="sxs-lookup"><span data-stu-id="6be30-183">b.</span></span> <span data-ttu-id="6be30-184">Ouvrez dans le Bloc-notes votre certificat codé en base 64 téléchargé à partir du portail Azure, copiez son contenu dans le Presse-papiers, puis collez-le dans la zone de texte **Certificat OpenSSL** .</span><span class="sxs-lookup"><span data-stu-id="6be30-184">Open your Base64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **OpenSSL Certificate** textbox.</span></span>
   
    <span data-ttu-id="6be30-185">c.</span><span class="sxs-lookup"><span data-stu-id="6be30-185">c.</span></span> <span data-ttu-id="6be30-186">Dans la zone de texte URL SAML SSO, tapez `https://<your subdomain>.deputy.com/exec/devapp/samlacs?dpLoginTo=<saml sso url>`</span><span class="sxs-lookup"><span data-stu-id="6be30-186">In the SAML SSO URL textbox, type `https://<your subdomain>.deputy.com/exec/devapp/samlacs?dpLoginTo=<saml sso url>`</span></span>
    
    <span data-ttu-id="6be30-187">d.</span><span class="sxs-lookup"><span data-stu-id="6be30-187">d.</span></span> <span data-ttu-id="6be30-188">Dans la zone de texte URL SAML SSO, remplacez `<your subdomain>` par votre sous-domaine.</span><span class="sxs-lookup"><span data-stu-id="6be30-188">In the SAML SSO URL textbox, replace `<your subdomain>` with your subdomain.</span></span>
   
    <span data-ttu-id="6be30-189">e.</span><span class="sxs-lookup"><span data-stu-id="6be30-189">e.</span></span> <span data-ttu-id="6be30-190">Dans la zone de texte URL SAML SSO, remplacez `<saml sso url>` par **l’URL du service d’authentification unique SAML** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="6be30-190">In the SAML SSO URL textbox, replace `<saml sso url>` with the **SAML Single Sign-On Service URL** you have copied from the Azure portal.</span></span>
   
    <span data-ttu-id="6be30-191">f.</span><span class="sxs-lookup"><span data-stu-id="6be30-191">f.</span></span> <span data-ttu-id="6be30-192">Cliquez sur **Save Settings**.</span><span class="sxs-lookup"><span data-stu-id="6be30-192">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="6be30-193">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="6be30-193">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6be30-194">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="6be30-194">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6be30-195">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6be30-195">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6be30-196">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="6be30-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="6be30-197">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="6be30-197">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="6be30-199">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6be30-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6be30-200">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6be30-200">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6be30-202">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="6be30-202">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6be30-204">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="6be30-204">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6be30-206">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="6be30-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6be30-208">a.</span><span class="sxs-lookup"><span data-stu-id="6be30-208">a.</span></span> <span data-ttu-id="6be30-209">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6be30-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6be30-210">b.</span><span class="sxs-lookup"><span data-stu-id="6be30-210">b.</span></span> <span data-ttu-id="6be30-211">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6be30-211">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6be30-212">c.</span><span class="sxs-lookup"><span data-stu-id="6be30-212">c.</span></span> <span data-ttu-id="6be30-213">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="6be30-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6be30-214">d.</span><span class="sxs-lookup"><span data-stu-id="6be30-214">d.</span></span> <span data-ttu-id="6be30-215">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="6be30-215">Click **Create**.</span></span>
 
### <a name="creating-a-deputy-test-user"></a><span data-ttu-id="6be30-216">Création d’un utilisateur de test Deputy</span><span class="sxs-lookup"><span data-stu-id="6be30-216">Creating a Deputy test user</span></span>

<span data-ttu-id="6be30-217">Pour se connecter à Deputy, les utilisateurs d’Azure AD doivent être approvisionnés dans Deputy.</span><span class="sxs-lookup"><span data-stu-id="6be30-217">To enable Azure AD users to log in to Deputy, they must be provisioned into Deputy.</span></span> <span data-ttu-id="6be30-218">Dans le cas de Deputy, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="6be30-218">In case of Deputy, provisioning is a manual task.</span></span>

#### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="6be30-219">Pour approvisionner un compte d’utilisateur, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="6be30-219">To provision a user account, perform the following steps:</span></span>
1. <span data-ttu-id="6be30-220">Connectez-vous à votre site d’entreprise Deputy en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="6be30-220">Log in to your Deputy company site as an administrator.</span></span>

2. <span data-ttu-id="6be30-221">Dans le volet de navigation situé en haut, cliquez sur **People**(Personnes).</span><span class="sxs-lookup"><span data-stu-id="6be30-221">On the top navigation pane, click **People**.</span></span>
   
   <span data-ttu-id="6be30-222">![Personnes](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_001.png "Personnes")</span><span class="sxs-lookup"><span data-stu-id="6be30-222">![People](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_001.png "People")</span></span>

3. <span data-ttu-id="6be30-223">Cliquez sur le bouton **Add People** (Ajouter des personnes), puis cliquez sur **Add a single person** (Ajouter une seule personne).</span><span class="sxs-lookup"><span data-stu-id="6be30-223">Click the **Add People** button and click **Add a single person**.</span></span>
   
   <span data-ttu-id="6be30-224">![Ajouter des personnes](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_002.png "ajouter des personnes")</span><span class="sxs-lookup"><span data-stu-id="6be30-224">![Add People](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_002.png "Add People")</span></span>

4. <span data-ttu-id="6be30-225">Effectuez les opérations suivantes, puis cliquez sur **Save & Invite** (Enregistrer et inviter).</span><span class="sxs-lookup"><span data-stu-id="6be30-225">Perform the following steps and click **Save & Invite**.</span></span>
   
   <span data-ttu-id="6be30-226">![Nouvel utilisateur](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_003.png "Nouvel utilisateur")</span><span class="sxs-lookup"><span data-stu-id="6be30-226">![New User](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_003.png "New User")</span></span>

   <span data-ttu-id="6be30-227">a.</span><span class="sxs-lookup"><span data-stu-id="6be30-227">a.</span></span> <span data-ttu-id="6be30-228">Dans la zone de texte **Nom**, entrez le nom de l’utilisateur, par exemple **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="6be30-228">In the **Name** textbox, type name of the user like **BrittaSimon**.</span></span>
   
   <span data-ttu-id="6be30-229">b.</span><span class="sxs-lookup"><span data-stu-id="6be30-229">b.</span></span> <span data-ttu-id="6be30-230">Dans la zone de texte **Email** , tapez l’adresse de messagerie du compte Azure AD que vous souhaitez approvisionner.</span><span class="sxs-lookup"><span data-stu-id="6be30-230">In the **Email** textbox, type the email address of an Azure AD account you want to provision.</span></span>
   
   <span data-ttu-id="6be30-231">c.</span><span class="sxs-lookup"><span data-stu-id="6be30-231">c.</span></span> <span data-ttu-id="6be30-232">Dans la zone de texte **Travaille chez**, tapez le nom de l’entreprise.</span><span class="sxs-lookup"><span data-stu-id="6be30-232">In the **Work at** textbox, type the business name.</span></span>
   
   <span data-ttu-id="6be30-233">d.</span><span class="sxs-lookup"><span data-stu-id="6be30-233">d.</span></span> <span data-ttu-id="6be30-234">Cliquez sur le bouton **Save & Invite**.</span><span class="sxs-lookup"><span data-stu-id="6be30-234">Click **Save & Invite** button.</span></span>

5. <span data-ttu-id="6be30-235">Le détenteur du compte AAD reçoit un message électronique et suit un lien pour confirmer le compte avant qu’il ne soit activé.</span><span class="sxs-lookup"><span data-stu-id="6be30-235">The AAD account holder receives an email and follows a link to confirm their account before it becomes active.</span></span> <span data-ttu-id="6be30-236">Vous pouvez utiliser n’importe quel autre outil ou API de création de compte d’utilisateur fourni par Deputy pour approvisionner des comptes d’utilisateurs AAD.</span><span class="sxs-lookup"><span data-stu-id="6be30-236">You can use any other Deputy user account creation tools or APIs provided by Deputy to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6be30-237">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="6be30-237">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6be30-238">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Deputy.</span><span class="sxs-lookup"><span data-stu-id="6be30-238">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Deputy.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="6be30-240">**Pour affecter Britta Simon à Deputy, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="6be30-240">**To assign Britta Simon to Deputy, perform the following steps:**</span></span>

1. <span data-ttu-id="6be30-241">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="6be30-241">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="6be30-243">Dans la liste des applications, sélectionnez **Deputy**.</span><span class="sxs-lookup"><span data-stu-id="6be30-243">In the applications list, select **Deputy**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_app.png) 

3. <span data-ttu-id="6be30-245">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="6be30-245">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="6be30-247">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="6be30-247">Click **Add** button.</span></span> <span data-ttu-id="6be30-248">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="6be30-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="6be30-250">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="6be30-250">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6be30-251">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="6be30-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6be30-252">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="6be30-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6be30-253">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="6be30-253">Testing single sign-on</span></span>

<span data-ttu-id="6be30-254">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="6be30-254">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="6be30-255">Lorsque vous cliquez sur la vignette Deputy dans le volet d’accès, vous devez être connecté automatiquement à votre application Deputy.</span><span class="sxs-lookup"><span data-stu-id="6be30-255">When you click the Deputy tile in the Access Panel, you should get automatically signed-on to your Deputy application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6be30-256">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="6be30-256">Additional resources</span></span>

* [<span data-ttu-id="6be30-257">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6be30-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6be30-258">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="6be30-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_203.png

