---
title: "Didacticiel : Intégration d’Azure Active Directory à 8x8 Virtual Office | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et 8x8 Virtual Office."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b34a6edf-e745-4aec-b0b2-7337473d64c5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: d8dcf0171b93fec15347e810a1b525bd815dbf04
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-8x8-virtual-office"></a><span data-ttu-id="9e39f-103">Didacticiel : Intégration d’Azure Active Directory à 8x8 Virtual Office</span><span class="sxs-lookup"><span data-stu-id="9e39f-103">Tutorial: Azure Active Directory integration with 8x8 Virtual Office</span></span>

<span data-ttu-id="9e39f-104">Dans ce didacticiel, vous allez apprendre à intégrer 8x8 Virtual Office à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9e39f-104">In this tutorial, you learn how to integrate 8x8 Virtual Office with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9e39f-105">L’intégration de 8x8 Virtual Office dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="9e39f-105">Integrating 8x8 Virtual Office with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9e39f-106">Dans Azure AD, vous pouvez contrôler qui a accès à 8x8 Virtual Office.</span><span class="sxs-lookup"><span data-stu-id="9e39f-106">You can control in Azure AD who has access to 8x8 Virtual Office</span></span>
- <span data-ttu-id="9e39f-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à 8x8 Virtual Office (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9e39f-107">You can enable your users to automatically get signed-on to 8x8 Virtual Office (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9e39f-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="9e39f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9e39f-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9e39f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9e39f-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="9e39f-110">Prerequisites</span></span>

<span data-ttu-id="9e39f-111">Pour configurer l’intégration d’Azure AD à 8x8 Virtual Office, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="9e39f-111">To configure Azure AD integration with 8x8 Virtual Office, you need the following items:</span></span>

- <span data-ttu-id="9e39f-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e39f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9e39f-113">Un abonnement 8x8 Virtual Office pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="9e39f-113">A 8x8 Virtual Office single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9e39f-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="9e39f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9e39f-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="9e39f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9e39f-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="9e39f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9e39f-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9e39f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9e39f-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="9e39f-118">Scenario description</span></span>
<span data-ttu-id="9e39f-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="9e39f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9e39f-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="9e39f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9e39f-121">Ajout de 8x8 Virtual Office à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="9e39f-121">Adding 8x8 Virtual Office from the gallery</span></span>
2. <span data-ttu-id="9e39f-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e39f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-8x8-virtual-office-from-the-gallery"></a><span data-ttu-id="9e39f-123">Ajout de 8x8 Virtual Office à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="9e39f-123">Adding 8x8 Virtual Office from the gallery</span></span>
<span data-ttu-id="9e39f-124">Pour configurer l’intégration de 8x8 Virtual Office avec Azure AD, vous devez ajouter 8x8 Virtual Office, disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="9e39f-124">To configure the integration of 8x8 Virtual Office into Azure AD, you need to add 8x8 Virtual Office from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9e39f-125">**Pour ajouter 8x8 Virtual Office à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9e39f-125">**To add 8x8 Virtual Office from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9e39f-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9e39f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9e39f-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="9e39f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9e39f-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="9e39f-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="9e39f-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="9e39f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="9e39f-133">Dans la zone de recherche, saisissez **8x8 Virtual Office**.</span><span class="sxs-lookup"><span data-stu-id="9e39f-133">In the search box, type **8x8 Virtual Office**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_search.png)

5. <span data-ttu-id="9e39f-135">Dans le volet des résultats, sélectionnez **8x8 Virtual Office**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="9e39f-135">In the results panel, select **8x8 Virtual Office**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9e39f-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e39f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9e39f-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec 8x8 Virtual Office, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="9e39f-138">In this section, you configure and test Azure AD single sign-on with 8x8 Virtual Office based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9e39f-139">Pour que l’authentification unique fonctionne, Azure AD doit connaître l’utilisateur 8x8 Virtual Office correspondant à l’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9e39f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 8x8 Virtual Office is to a user in Azure AD.</span></span> <span data-ttu-id="9e39f-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur 8x8 Virtual Office associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="9e39f-140">In other words, a link relationship between an Azure AD user and the related user in 8x8 Virtual Office needs to be established.</span></span>

<span data-ttu-id="9e39f-141">Dans 8x8 Virtual Office, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="9e39f-141">In 8x8 Virtual Office, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9e39f-142">Pour configurer et tester l’authentification unique Azure AD avec 8x8 Virtual Office, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="9e39f-142">To configure and test Azure AD single sign-on with 8x8 Virtual Office, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9e39f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="9e39f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9e39f-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9e39f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9e39f-145">**[Création d’un utilisateur de test 8x8 Virtual Office](#creating-a-8x8-virtual-office-test-user)** pour avoir un équivalent de Britta Simon dans 8x8 Virtual Office lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9e39f-145">**[Creating a 8x8 Virtual Office test user](#creating-a-8x8-virtual-office-test-user)** - to have a counterpart of Britta Simon in 8x8 Virtual Office that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9e39f-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9e39f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9e39f-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="9e39f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9e39f-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e39f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9e39f-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application 8x8 Virtual Office.</span><span class="sxs-lookup"><span data-stu-id="9e39f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 8x8 Virtual Office application.</span></span>

<span data-ttu-id="9e39f-150">**Pour configurer l’authentification unique Azure AD avec 8x8 Virtual Office, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="9e39f-150">**To configure Azure AD single sign-on with 8x8 Virtual Office, perform the following steps:**</span></span>

1. <span data-ttu-id="9e39f-151">Dans le portail Azure, dans la page d’intégration de l’application **8x8 Virtual Office**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="9e39f-151">In the Azure portal, on the **8x8 Virtual Office** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="9e39f-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="9e39f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_samlbase.png)

3. <span data-ttu-id="9e39f-155">Dans la section **Domaine et URL 8x8 Virtual Office**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="9e39f-155">On the **8x8 Virtual Office Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_url.png)

    <span data-ttu-id="9e39f-157">a.</span><span class="sxs-lookup"><span data-stu-id="9e39f-157">a.</span></span> <span data-ttu-id="9e39f-158">Dans la zone de texte **Identificateur**, entrez une URL au format suivant :</span><span class="sxs-lookup"><span data-stu-id="9e39f-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>

    <span data-ttu-id="9e39f-159">| `https://sso.8x8.com/<companyname>` |
    | `https://www.8x8.com/<companyname>` |
    | `https://sso.8x8pilot.com/<companyname>` |</span><span class="sxs-lookup"><span data-stu-id="9e39f-159">| `https://sso.8x8.com/<companyname>` |
 | `https://www.8x8.com/<companyname>` |
 | `https://sso.8x8pilot.com/<companyname>` |</span></span>

    <span data-ttu-id="9e39f-160">b.</span><span class="sxs-lookup"><span data-stu-id="9e39f-160">b.</span></span> <span data-ttu-id="9e39f-161">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant :</span><span class="sxs-lookup"><span data-stu-id="9e39f-161">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>

    <span data-ttu-id="9e39f-162">| `https://<subdomain>.8x8.com/saml2` |
    | `https://<subdomain>.8x8pilot.com/saml2`|</span><span class="sxs-lookup"><span data-stu-id="9e39f-162">| `https://<subdomain>.8x8.com/saml2` |
 | `https://<subdomain>.8x8pilot.com/saml2`|</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9e39f-163">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="9e39f-163">These values are not real.</span></span> <span data-ttu-id="9e39f-164">Mettez à jour ces valeurs avec l’identificateur et l’URL de réponse réels.</span><span class="sxs-lookup"><span data-stu-id="9e39f-164">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="9e39f-165">Pour obtenir ces valeurs, contactez [l’équipe du support 8x8 Virtual Office](https://www.8x8.com/about-us/contact-us).</span><span class="sxs-lookup"><span data-stu-id="9e39f-165">Contact [8x8 Virtual Office support team](https://www.8x8.com/about-us/contact-us) to get these values.</span></span>
 


4. <span data-ttu-id="9e39f-166">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (brut)**, puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="9e39f-166">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_certificate.png) 

5. <span data-ttu-id="9e39f-168">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="9e39f-168">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9e39f-170">Dans la section **Configuration de 8x8 Virtual Office**, cliquez sur **Configurer 8x8 Virtual Office** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="9e39f-170">On the **8x8 Virtual Office Configuration** section, click **Configure 8x8 Virtual Office** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9e39f-171">Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="9e39f-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_configure.png) 

7. <span data-ttu-id="9e39f-173">Connectez-vous à votre client 8x8 Virtual Office en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="9e39f-173">Sign-on to your 8x8 Virtual Office tenant as an administrator.</span></span>

8. <span data-ttu-id="9e39f-174">Sélectionnez **Virtual Office Account Mgr** (Gestionnaire de compte Virtual Office) dans le volet Applications.</span><span class="sxs-lookup"><span data-stu-id="9e39f-174">Select **Virtual Office Account Mgr** on Application Panel.</span></span>
   
    ![Configurer l’authentification côté application](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_001.png)

9. <span data-ttu-id="9e39f-176">Sélectionnez le compte **Entreprise** à gérer, puis cliquez sur le bouton **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="9e39f-176">Select **Business** account to manage and click **Sign In** button.</span></span>
   
    ![Configurer l’authentification côté application](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_002.png)

10. <span data-ttu-id="9e39f-178">Cliquez sur l’onglet **Comptes** dans la liste de menu.</span><span class="sxs-lookup"><span data-stu-id="9e39f-178">Click **Accounts** tab in the menu list.</span></span>
   
    ![Configurer l’authentification côté application](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_003.png)

11. <span data-ttu-id="9e39f-180">Cliquez sur **Authentification unique** dans la liste des comptes.</span><span class="sxs-lookup"><span data-stu-id="9e39f-180">Click **Single Sign On** in the list of Accounts.</span></span>
   
    ![Configurer l’authentification côté application](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_004.png)

12. <span data-ttu-id="9e39f-182">Sélectionnez **Authentification unique** sous la section Méthode d’authentification, puis cliquez sur **SAML**.</span><span class="sxs-lookup"><span data-stu-id="9e39f-182">Select **Single Sign On** under Authentication method and click **SAML**.</span></span>
    
    ![Configurer l’authentification côté application](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_005.png)

13. <span data-ttu-id="9e39f-184">Copiez **l’URL d’authentification unique SAML**, **l’URL du service d’authentification unique** et **l’URL de l’émetteur** d’Azure AD dans les champs **URL de connexion**, **URL de déconnexion** et **URL de l’émetteur** de 8x8 Virtual Office.</span><span class="sxs-lookup"><span data-stu-id="9e39f-184">Copy **SAML SSO URL**, **Single Sing Out Service URL** and **Issuer URL** from Azure AD to **Sign In URL**, **Sign Out URL** and **Issuer URL** in 8x8 Virtual Office.</span></span> 
    
    ![Configurer l’authentification côté application](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_006.png)
    
14. <span data-ttu-id="9e39f-186">Cliquez sur le bouton **Explorateur** pour charger le certificat que vous avez téléchargé à partir d’Azure AD, puis cliquez sur le bouton **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="9e39f-186">Click **Browser** button to upload the certificate which you downloaded from Azure AD, and click the **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="9e39f-187">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="9e39f-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9e39f-188">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="9e39f-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9e39f-189">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9e39f-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9e39f-190">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e39f-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="9e39f-191">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="9e39f-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="9e39f-193">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9e39f-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9e39f-194">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9e39f-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9e39f-196">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="9e39f-196">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9e39f-198">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="9e39f-198">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9e39f-200">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="9e39f-200">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-8x8virtualoffice-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9e39f-202">a.</span><span class="sxs-lookup"><span data-stu-id="9e39f-202">a.</span></span> <span data-ttu-id="9e39f-203">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9e39f-203">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9e39f-204">b.</span><span class="sxs-lookup"><span data-stu-id="9e39f-204">b.</span></span> <span data-ttu-id="9e39f-205">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9e39f-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9e39f-206">c.</span><span class="sxs-lookup"><span data-stu-id="9e39f-206">c.</span></span> <span data-ttu-id="9e39f-207">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="9e39f-207">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9e39f-208">d.</span><span class="sxs-lookup"><span data-stu-id="9e39f-208">d.</span></span> <span data-ttu-id="9e39f-209">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="9e39f-209">Click **Create**.</span></span>
 
### <a name="creating-a-8x8-virtual-office-test-user"></a><span data-ttu-id="9e39f-210">Création d’un utilisateur de test 8x8 Virtual Office</span><span class="sxs-lookup"><span data-stu-id="9e39f-210">Creating a 8x8 Virtual Office test user</span></span>

<span data-ttu-id="9e39f-211">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans 8x8 Virtual Office.</span><span class="sxs-lookup"><span data-stu-id="9e39f-211">The objective of this section is to create a user called Britta Simon in 8x8 Virtual Office.</span></span> <span data-ttu-id="9e39f-212">8x8 Virtual Office prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="9e39f-212">8x8 Virtual Office supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="9e39f-213">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="9e39f-213">There is no action item for you in this section.</span></span> <span data-ttu-id="9e39f-214">Un utilisateur est créé lors d’une tentative d’accès à 8x8 Virtual Office s’il n’existe pas déjà.</span><span class="sxs-lookup"><span data-stu-id="9e39f-214">A new user is created during an attempt to access 8x8 Virtual Office if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="9e39f-215">Si vous devez créer un utilisateur manuellement, contactez [l’équipe du support technique 8x8 Virtual Office](https://www.8x8.com/about-us/contact-us).</span><span class="sxs-lookup"><span data-stu-id="9e39f-215">If you need to create a user manually, you need to contact the [8x8 Virtual Office support team](https://www.8x8.com/about-us/contact-us).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9e39f-216">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="9e39f-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9e39f-217">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à 8x8 Virtual Office.</span><span class="sxs-lookup"><span data-stu-id="9e39f-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 8x8 Virtual Office.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="9e39f-219">**Pour affecter Britta Simon à 8x8 Virtual Office, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="9e39f-219">**To assign Britta Simon to 8x8 Virtual Office, perform the following steps:**</span></span>

1. <span data-ttu-id="9e39f-220">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="9e39f-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="9e39f-222">Dans la liste des applications, sélectionnez **8x8 Virtual Office**.</span><span class="sxs-lookup"><span data-stu-id="9e39f-222">In the applications list, select **8x8 Virtual Office**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_8x8virtualoffice_app.png) 

3. <span data-ttu-id="9e39f-224">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="9e39f-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="9e39f-226">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="9e39f-226">Click **Add** button.</span></span> <span data-ttu-id="9e39f-227">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="9e39f-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="9e39f-229">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="9e39f-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9e39f-230">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="9e39f-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9e39f-231">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="9e39f-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9e39f-232">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="9e39f-232">Testing single sign-on</span></span>

<span data-ttu-id="9e39f-233">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="9e39f-233">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9e39f-234">Lorsque vous cliquez sur la vignette 8x8 Virtual Office dans le volet d’accès, vous devez être connecté automatiquement à votre application 8x8 Virtual Office.</span><span class="sxs-lookup"><span data-stu-id="9e39f-234">When you click the 8x8 Virtual Office tile in the Access Panel, you should get automatically signed-on to your 8x8 Virtual Office application.</span></span>
<span data-ttu-id="9e39f-235">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9e39f-235">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9e39f-236">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="9e39f-236">Additional resources</span></span>

* [<span data-ttu-id="9e39f-237">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9e39f-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9e39f-238">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="9e39f-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-8x8virtualoffice-tutorial/tutorial_general_203.png

