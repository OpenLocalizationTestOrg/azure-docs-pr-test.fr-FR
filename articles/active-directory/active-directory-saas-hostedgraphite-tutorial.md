---
title: "Didacticiel : Intégration d’Azure Active Directory à Hosted Graphite | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Hosted Graphite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a1ac4d7f-d079-4f3c-b6da-0f520d427ceb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: f6ed02cc67be4090402a115c30819ff6cff99c99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hosted-graphite"></a><span data-ttu-id="68ff8-103">Didacticiel : Intégration d’Azure Active Directory à Hosted Graphite</span><span class="sxs-lookup"><span data-stu-id="68ff8-103">Tutorial: Azure Active Directory integration with Hosted Graphite</span></span>

<span data-ttu-id="68ff8-104">Dans ce didacticiel, vous allez apprendre à intégrer Hosted Graphite à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="68ff8-104">In this tutorial, you learn how to integrate Hosted Graphite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="68ff8-105">L’intégration de Hosted Graphite à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="68ff8-105">Integrating Hosted Graphite with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="68ff8-106">Dans Azure AD, vous pouvez contrôler qui a accès à Hosted Graphite.</span><span class="sxs-lookup"><span data-stu-id="68ff8-106">You can control in Azure AD who has access to Hosted Graphite</span></span>
- <span data-ttu-id="68ff8-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Hosted Graphite (par le biais de l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="68ff8-107">You can enable your users to automatically get signed-on to Hosted Graphite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="68ff8-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="68ff8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="68ff8-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="68ff8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="68ff8-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="68ff8-110">Prerequisites</span></span>

<span data-ttu-id="68ff8-111">Pour configurer l’intégration d’Azure AD à Hosted Graphite, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="68ff8-111">To configure Azure AD integration with Hosted Graphite, you need the following items:</span></span>

- <span data-ttu-id="68ff8-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="68ff8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="68ff8-113">Un abonnement Hosted Graphite pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="68ff8-113">A Hosted Graphite single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="68ff8-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="68ff8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="68ff8-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="68ff8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="68ff8-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="68ff8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="68ff8-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="68ff8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="68ff8-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="68ff8-118">Scenario description</span></span>
<span data-ttu-id="68ff8-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="68ff8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="68ff8-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="68ff8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="68ff8-121">Ajout de Hosted Graphite à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="68ff8-121">Adding Hosted Graphite from the gallery</span></span>
2. <span data-ttu-id="68ff8-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="68ff8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hosted-graphite-from-the-gallery"></a><span data-ttu-id="68ff8-123">Ajout de Hosted Graphite à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="68ff8-123">Adding Hosted Graphite from the gallery</span></span>
<span data-ttu-id="68ff8-124">Pour configurer l’intégration de Hosted Graphite à Azure AD, vous devez ajouter Hosted Graphite à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="68ff8-124">To configure the integration of Hosted Graphite into Azure AD, you need to add Hosted Graphite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="68ff8-125">**Pour ajouter Hosted Graphite à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="68ff8-125">**To add Hosted Graphite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="68ff8-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="68ff8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="68ff8-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="68ff8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="68ff8-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="68ff8-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="68ff8-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="68ff8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="68ff8-133">Dans la zone de recherche, tapez **Hosted Graphite**.</span><span class="sxs-lookup"><span data-stu-id="68ff8-133">In the search box, type **Hosted Graphite**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_search.png)

5. <span data-ttu-id="68ff8-135">Dans le volet des résultats, sélectionnez **Hosted Graphite**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="68ff8-135">In the results panel, select **Hosted Graphite**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="68ff8-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="68ff8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="68ff8-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Hosted Graphite avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="68ff8-138">In this section, you configure and test Azure AD single sign-on with Hosted Graphite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="68ff8-139">Pour que l’authentification unique fonctionne, Azure AD a besoin de savoir qui est l’utilisateur Hosted Graphite équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="68ff8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Hosted Graphite is to a user in Azure AD.</span></span> <span data-ttu-id="68ff8-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Hosted Graphite associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="68ff8-140">In other words, a link relationship between an Azure AD user and the related user in Hosted Graphite needs to be established.</span></span>

<span data-ttu-id="68ff8-141">Dans Hosted Graphite, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="68ff8-141">In Hosted Graphite, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="68ff8-142">Pour configurer et tester l’authentification unique Azure AD avec Hosted Graphite, vous avez besoin de suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="68ff8-142">To configure and test Azure AD single sign-on with Hosted Graphite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="68ff8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="68ff8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="68ff8-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="68ff8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="68ff8-145">**[Création d’un utilisateur de test Hosted Graphite](#creating-a-hosted-graphite-test-user)** pour avoir un équivalent de Britta Simon dans Hosted Graphite lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="68ff8-145">**[Creating a Hosted Graphite test user](#creating-a-hosted-graphite-test-user)** - to have a counterpart of Britta Simon in Hosted Graphite that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="68ff8-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="68ff8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="68ff8-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="68ff8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="68ff8-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="68ff8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="68ff8-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Hosted Graphite.</span><span class="sxs-lookup"><span data-stu-id="68ff8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Hosted Graphite application.</span></span>

<span data-ttu-id="68ff8-150">**Pour configurer l’authentification unique Azure AD avec Hosted Graphite, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="68ff8-150">**To configure Azure AD single sign-on with Hosted Graphite, perform the following steps:**</span></span>

1. <span data-ttu-id="68ff8-151">Dans le portail Azure, sur la page d’intégration de l’application **Hosted Graphite**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="68ff8-151">In the Azure portal, on the **Hosted Graphite** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="68ff8-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="68ff8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_samlbase.png)

3. <span data-ttu-id="68ff8-155">Dans la section **Domaine et URL Hosted Graphite**, si vous voulez configurer l’application en **Mode initié par IDP**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="68ff8-155">On the **Hosted Graphite Domain and URLs** section, if you wish to configure the application in **IDP initiated mode**, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_url.png)

    <span data-ttu-id="68ff8-157">a.</span><span class="sxs-lookup"><span data-stu-id="68ff8-157">a.</span></span> <span data-ttu-id="68ff8-158">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://www.hostedgraphite.com/metadata/<user id>`</span><span class="sxs-lookup"><span data-stu-id="68ff8-158">In the **Identifier** textbox, type a URL using the following pattern: `https://www.hostedgraphite.com/metadata/<user id>`</span></span>

    <span data-ttu-id="68ff8-159">b.</span><span class="sxs-lookup"><span data-stu-id="68ff8-159">b.</span></span> <span data-ttu-id="68ff8-160">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://www.hostedgraphite.com/complete/saml/<user id>`</span><span class="sxs-lookup"><span data-stu-id="68ff8-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://www.hostedgraphite.com/complete/saml/<user id>`</span></span>

4. <span data-ttu-id="68ff8-161">Dans la section **Domaine et URL Hosted Graphite**, si vous voulez configurer l’application en **Mode initié par SP**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="68ff8-161">On the **Hosted Graphite Domain and URLs** section, if you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_10.png)
  
    <span data-ttu-id="68ff8-163">a.</span><span class="sxs-lookup"><span data-stu-id="68ff8-163">a.</span></span> <span data-ttu-id="68ff8-164">Cliquez sur l’option **Afficher les paramètres d’URL avancés**.</span><span class="sxs-lookup"><span data-stu-id="68ff8-164">Click on the **Show advanced URL settings** option</span></span>

    <span data-ttu-id="68ff8-165">b.</span><span class="sxs-lookup"><span data-stu-id="68ff8-165">b.</span></span> <span data-ttu-id="68ff8-166">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://www.hostedgraphite.com/login/saml/<user id>/`</span><span class="sxs-lookup"><span data-stu-id="68ff8-166">In the **Sign On URL** textbox, type a URL using the following pattern: `https://www.hostedgraphite.com/login/saml/<user id>/`</span></span>   

    > [!NOTE] 
    > <span data-ttu-id="68ff8-167">Notez qu’il ne s’agit pas des valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="68ff8-167">Please note that these are not the real values.</span></span> <span data-ttu-id="68ff8-168">Vous devez mettre à jour ces valeurs avec l’identificateur, l’URL de réponse et l’URL de connexion réels.</span><span class="sxs-lookup"><span data-stu-id="68ff8-168">You have to update these values with the actual Identifier, Reply URL and Sign On URL.</span></span> <span data-ttu-id="68ff8-169">Pour obtenir ces valeurs, vous pouvez accéder à Accéder->Configuration de SAML ou contactez [l’équipe de support d’Hosted Graphite](mailto:help@hostedgraphite.com).</span><span class="sxs-lookup"><span data-stu-id="68ff8-169">To get these values, you can go to Access->SAML setup on your Application side or Contact [Hosted Graphite support team](mailto:help@hostedgraphite.com).</span></span>
    >
 
5. <span data-ttu-id="68ff8-170">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="68ff8-170">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_certificate.png) 

6. <span data-ttu-id="68ff8-172">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="68ff8-172">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="68ff8-174">Dans la section **Configuration d’Hosted Graphite**, cliquez sur **Configurer Hosted Graphite** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="68ff8-174">On the **Hosted Graphite Configuration** section, click **Configure Hosted Graphite** to open **Configure sign-on** window.</span></span> <span data-ttu-id="68ff8-175">Copiez **l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="68ff8-175">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_configure.png) 

8. <span data-ttu-id="68ff8-177">Connectez-vous à votre client Hosted Graphite en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="68ff8-177">Sign-on to your Hosted Graphite tenant as an administrator.</span></span>

9. <span data-ttu-id="68ff8-178">Accédez à la **page de configuration de SAML** dans la barre latérale (**Accéder -> Configuration SAML**).</span><span class="sxs-lookup"><span data-stu-id="68ff8-178">Go to the **SAML Setup page** in the sidebar (**Access -> SAML Setup**).</span></span>
   
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_000.png)

10. <span data-ttu-id="68ff8-180">Confirmez que ces URL correspondent à votre configuration de la section **Domaine et URL Hosted Graphite** du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="68ff8-180">Confirm these URls match your configuration done on the **Hosted Graphite Domain and URLs** section of the Azure portal.</span></span>
   
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_001.png)

11. <span data-ttu-id="68ff8-182">Dans les zones de texte **ID d’entité ou d’émetteur** et **URL de connexion à authentification unique**, collez les valeurs **ID d’entité SAML** et **URL du service d’authentification unique SAML** que vous avez copiées à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="68ff8-182">In  **Entity or Issuer ID** and **SSO Login URL** textboxes, paste the value of **SAML Entity ID** and **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 
   
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_002.png)
   

12. <span data-ttu-id="68ff8-184">Sélectionnez « **Lecture seule** » comme **Rôle d’utilisateur par défaut**.</span><span class="sxs-lookup"><span data-stu-id="68ff8-184">Select "**Read-only**" as **Default User Role**.</span></span>
    
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_004.png)

13. <span data-ttu-id="68ff8-186">Ouvrez dans le Bloc-notes votre certificat codé en base 64 téléchargé à partir du portail Azure, copiez son contenu dans le Presse-papiers, puis collez-le dans la zone de texte **Certificat X.509**.</span><span class="sxs-lookup"><span data-stu-id="68ff8-186">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox.</span></span>
    
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_005.png)

14. <span data-ttu-id="68ff8-188">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="68ff8-188">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="68ff8-189">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="68ff8-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="68ff8-190">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="68ff8-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="68ff8-191">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="68ff8-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="68ff8-192">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="68ff8-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="68ff8-193">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="68ff8-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="68ff8-195">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="68ff8-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="68ff8-196">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="68ff8-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="68ff8-198">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="68ff8-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="68ff8-200">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="68ff8-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="68ff8-202">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="68ff8-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hostedgraphite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="68ff8-204">a.</span><span class="sxs-lookup"><span data-stu-id="68ff8-204">a.</span></span> <span data-ttu-id="68ff8-205">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="68ff8-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="68ff8-206">b.</span><span class="sxs-lookup"><span data-stu-id="68ff8-206">b.</span></span> <span data-ttu-id="68ff8-207">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="68ff8-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="68ff8-208">c.</span><span class="sxs-lookup"><span data-stu-id="68ff8-208">c.</span></span> <span data-ttu-id="68ff8-209">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="68ff8-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="68ff8-210">d.</span><span class="sxs-lookup"><span data-stu-id="68ff8-210">d.</span></span> <span data-ttu-id="68ff8-211">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="68ff8-211">Click **Create**.</span></span>
 
### <a name="creating-a-hosted-graphite-test-user"></a><span data-ttu-id="68ff8-212">Création d’un utilisateur de test Hosted Graphite</span><span class="sxs-lookup"><span data-stu-id="68ff8-212">Creating a Hosted Graphite test user</span></span>

<span data-ttu-id="68ff8-213">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans Hosted Graphite.</span><span class="sxs-lookup"><span data-stu-id="68ff8-213">The objective of this section is to create a user called Britta Simon in Hosted Graphite.</span></span> <span data-ttu-id="68ff8-214">Hosted Graphite prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="68ff8-214">Hosted Graphite supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="68ff8-215">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="68ff8-215">There is no action item for you in this section.</span></span> <span data-ttu-id="68ff8-216">Un utilisateur est créé lors d’une tentative d’accès à Hosted Graphite s’il n’existe pas déjà.</span><span class="sxs-lookup"><span data-stu-id="68ff8-216">A new user will be created during an attempt to access Hosted Graphite if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="68ff8-217">Si vous devez créer un utilisateur manuellement, contactez l’équipe de support d’Hosted Graphite via <mailto:help@hostedgraphite.com>.</span><span class="sxs-lookup"><span data-stu-id="68ff8-217">If you need to create a user manually, you need to contact the Hosted Graphite support team via <mailto:help@hostedgraphite.com>.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="68ff8-218">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="68ff8-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="68ff8-219">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Hosted Graphite.</span><span class="sxs-lookup"><span data-stu-id="68ff8-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Hosted Graphite.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="68ff8-221">**Pour affecter Britta Simon à Hosted Graphite, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="68ff8-221">**To assign Britta Simon to Hosted Graphite, perform the following steps:**</span></span>

1. <span data-ttu-id="68ff8-222">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="68ff8-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="68ff8-224">Dans la liste des applications, sélectionnez **Hosted Graphite**.</span><span class="sxs-lookup"><span data-stu-id="68ff8-224">In the applications list, select **Hosted Graphite**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hostedgraphite-tutorial/tutorial_hostedgraphite_app.png) 

3. <span data-ttu-id="68ff8-226">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="68ff8-226">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="68ff8-228">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="68ff8-228">Click **Add** button.</span></span> <span data-ttu-id="68ff8-229">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="68ff8-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="68ff8-231">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="68ff8-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="68ff8-232">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="68ff8-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="68ff8-233">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="68ff8-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="68ff8-234">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="68ff8-234">Testing single sign-on</span></span>

<span data-ttu-id="68ff8-235">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="68ff8-235">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="68ff8-236">Quand vous cliquez sur la vignette Hosted Graphite dans le volet d’accès, vous devez être connecté automatiquement à votre application Hosted Graphite.</span><span class="sxs-lookup"><span data-stu-id="68ff8-236">When you click the Hosted Graphite tile in the Access Panel, you should get automatically signed-on to your Hosted Graphite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="68ff8-237">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="68ff8-237">Additional resources</span></span>

* [<span data-ttu-id="68ff8-238">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="68ff8-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="68ff8-239">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="68ff8-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hostedgraphite-tutorial/tutorial_general_203.png

