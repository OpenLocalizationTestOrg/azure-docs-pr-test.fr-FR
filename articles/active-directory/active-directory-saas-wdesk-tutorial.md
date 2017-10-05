---
title: "Didacticiel : Intégration d’Azure Active Directory à Wdesk | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Wdesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 06900a91-a326-4663-8ba6-69ae741a536e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 37660b80cfb01d6a3105aea5ce248f1e03c46695
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wdesk"></a><span data-ttu-id="b234f-103">Didacticiel : Intégration d’Azure Active Directory à Wdesk</span><span class="sxs-lookup"><span data-stu-id="b234f-103">Tutorial: Azure Active Directory integration with Wdesk</span></span>

<span data-ttu-id="b234f-104">Ce didacticiel vous montrera comment intégrer Wdesk à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b234f-104">In this tutorial, you learn how to integrate Wdesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b234f-105">L’intégration de Wdesk dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="b234f-105">Integrating Wdesk with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b234f-106">Dans Azure AD, vous pouvez contrôler qui a accès à Wdesk</span><span class="sxs-lookup"><span data-stu-id="b234f-106">You can control in Azure AD who has access to Wdesk</span></span>
- <span data-ttu-id="b234f-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Wdesk (via l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="b234f-107">You can enable your users to automatically get signed-on to Wdesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b234f-108">Vous pouvez gérer vos comptes depuis un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="b234f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b234f-109">Pour en savoir plus sur l’intégration de l’application SaaS avec Azure AD, consultez</span><span class="sxs-lookup"><span data-stu-id="b234f-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="b234f-110">[Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b234f-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b234f-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b234f-111">Prerequisites</span></span>

<span data-ttu-id="b234f-112">Pour configurer l’intégration d’Azure AD avec Wdesk, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="b234f-112">To configure Azure AD integration with Wdesk, you need the following items:</span></span>

- <span data-ttu-id="b234f-113">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="b234f-113">An Azure AD subscription</span></span>
- <span data-ttu-id="b234f-114">Un abonnement Wdesk avec authentification unique activée</span><span class="sxs-lookup"><span data-stu-id="b234f-114">A Wdesk single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b234f-115">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="b234f-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b234f-116">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="b234f-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b234f-117">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="b234f-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b234f-118">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b234f-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b234f-119">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="b234f-119">Scenario description</span></span>
<span data-ttu-id="b234f-120">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="b234f-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b234f-121">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="b234f-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b234f-122">Ajout de Wdesk depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="b234f-122">Adding Wdesk from the gallery</span></span>
2. <span data-ttu-id="b234f-123">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b234f-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-wdesk-from-the-gallery"></a><span data-ttu-id="b234f-124">Ajout de Wdesk depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="b234f-124">Adding Wdesk from the gallery</span></span>
<span data-ttu-id="b234f-125">Pour configurer l’intégration de Wdesk avec Azure AD, vous devez ajouter Wdesk à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="b234f-125">To configure the integration of Wdesk into Azure AD, you need to add Wdesk from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b234f-126">**Pour ajouter Wdesk à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b234f-126">**To add Wdesk from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b234f-127">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b234f-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b234f-129">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="b234f-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b234f-130">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="b234f-130">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="b234f-132">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="b234f-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="b234f-134">Dans la zone de recherche, tapez **Wdesk**.</span><span class="sxs-lookup"><span data-stu-id="b234f-134">In the search box, type **Wdesk**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_search.png)

5. <span data-ttu-id="b234f-136">Dans le volet de résultats, sélectionnez **Wdesk**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="b234f-136">In the results panel, select **Wdesk**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b234f-138">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b234f-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b234f-139">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Wdesk, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="b234f-139">In this section, you configure and test Azure AD single sign-on with Wdesk based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b234f-140">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Wdesk correspondant dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b234f-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Wdesk is to a user in Azure AD.</span></span> <span data-ttu-id="b234f-141">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Wdesk associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="b234f-141">In other words, a link relationship between an Azure AD user and the related user in Wdesk needs to be established.</span></span>

<span data-ttu-id="b234f-142">Pour cela, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** dans Wdesk.</span><span class="sxs-lookup"><span data-stu-id="b234f-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Wdesk.</span></span>

<span data-ttu-id="b234f-143">Pour configurer et tester l’authentification unique Azure AD avec Wdesk, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="b234f-143">To configure and test Azure AD single sign-on with Wdesk, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b234f-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="b234f-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b234f-145">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b234f-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b234f-146">**[Création d’un utilisateur de test Wdesk](#creating-a-wdesk-test-user)** pour avoir un équivalent de Britta Simon dans Wdesk lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b234f-146">**[Creating a Wdesk test user](#creating-a-wdesk-test-user)** - to have a counterpart of Britta Simon in Wdesk that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b234f-147">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b234f-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b234f-148">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="b234f-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b234f-149">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b234f-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b234f-150">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Wdesk.</span><span class="sxs-lookup"><span data-stu-id="b234f-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Wdesk application.</span></span>

<span data-ttu-id="b234f-151">**Pour configurer l’authentification unique Azure AD avec Wdesk, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b234f-151">**To configure Azure AD single sign-on with Wdesk, perform the following steps:**</span></span>

1. <span data-ttu-id="b234f-152">Dans le portail Azure, sur la page d’intégration de l’application **Wdesk**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="b234f-152">In the Azure portal, on the **Wdesk** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="b234f-154">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="b234f-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_samlbase.png)

3. <span data-ttu-id="b234f-156">Dans la section **Domaines et URL Wdesk**, si vous souhaitez configurer l’application en Mode initié par **IDP**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="b234f-156">On the **Wdesk Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url.png)

    <span data-ttu-id="b234f-158">a.</span><span class="sxs-lookup"><span data-stu-id="b234f-158">a.</span></span> <span data-ttu-id="b234f-159">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<subdomain>.wdesk.com/auth/saml/sp/metadata/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="b234f-159">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.wdesk.com/auth/saml/sp/metadata/<instancename>`</span></span>

    <span data-ttu-id="b234f-160">b.</span><span class="sxs-lookup"><span data-stu-id="b234f-160">b.</span></span> <span data-ttu-id="b234f-161">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://<subdomain>.wdesk.com/auth/saml/sp/consumer/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="b234f-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.wdesk.com/auth/saml/sp/consumer/<instancename>`</span></span>

4. <span data-ttu-id="b234f-162">Cliquez sur **Afficher les paramètres d’URL avancés**.</span><span class="sxs-lookup"><span data-stu-id="b234f-162">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="b234f-163">Si vous souhaitez configurer l’application en mode initié par le **fournisseur de service**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="b234f-163">If you wish to configure the application in **SP** initiated mode, perform the following step:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_url1.png)

    <span data-ttu-id="b234f-165">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<subdomain>.wdesk.com/auth/login/saml/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="b234f-165">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.wdesk.com/auth/login/saml/<instancename>`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="b234f-166">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="b234f-166">These values are not real.</span></span> <span data-ttu-id="b234f-167">Mettez à jour ces valeurs avec l’identificateur, l’URL de réponse et l’URL de connexion réels.</span><span class="sxs-lookup"><span data-stu-id="b234f-167">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="b234f-168">Vous obtenez ces valeurs depuis le portail WDesk lorsque vous configurez l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="b234f-168">You get these values from WDesk portal when you configure the SSO.</span></span> 
  
5. <span data-ttu-id="b234f-169">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="b234f-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_certificate.png) 

6. <span data-ttu-id="b234f-171">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="b234f-171">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-wdesk-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="b234f-173">Ouvrez une autre fenêtre de navigateur web, puis connectez-vous à Wdesk en tant qu’administrateur de la sécurité.</span><span class="sxs-lookup"><span data-stu-id="b234f-173">In a different web browser window, login to Wdesk as a Security Administrator.</span></span>

8. <span data-ttu-id="b234f-174">En bas à gauche, cliquez sur **administrateur** et sélectionnez **Administrateur de compte** :</span><span class="sxs-lookup"><span data-stu-id="b234f-174">In the bottom left, click **Admin** and choose **Account Admin**:</span></span>
 
     ![Configurer l’authentification unique](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

9. <span data-ttu-id="b234f-176">Dans Administrateur Wdesk, accédez à **Sécurité**, puis **SAML** > **Paramètres SAML** :</span><span class="sxs-lookup"><span data-stu-id="b234f-176">In Wdesk Admin, navigate to **Security**, then **SAML** > **SAML Settings**:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig2.png)

10. <span data-ttu-id="b234f-178">Dans **Paramètres généraux**, cochez l’option **Activer l’authentification unique SAML** :</span><span class="sxs-lookup"><span data-stu-id="b234f-178">Under **General Settings**, check the **Enable SAML Single Sign On**:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig3.png)

11. <span data-ttu-id="b234f-180">Dans **Détails sur le fournisseur de services**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="b234f-180">Under **Service Provider Details**, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig4.png)

      <span data-ttu-id="b234f-182">a.</span><span class="sxs-lookup"><span data-stu-id="b234f-182">a.</span></span> <span data-ttu-id="b234f-183">Copiez l’**URL de connexion** et collez-la dans la zone de texte **URL d’authentification** sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="b234f-183">Copy the **Login URL** and paste it in **Sign-on Url** textbox on Azure portal.</span></span>
   
      <span data-ttu-id="b234f-184">b.</span><span class="sxs-lookup"><span data-stu-id="b234f-184">b.</span></span> <span data-ttu-id="b234f-185">Copiez l’**URL de métadonnée** et collez-la dans la zone de texte **Identificateur** sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="b234f-185">Copy the **Metadata Url** and paste it in **Identifier** textbox on Azure portal.</span></span>
       
      <span data-ttu-id="b234f-186">c.</span><span class="sxs-lookup"><span data-stu-id="b234f-186">c.</span></span> <span data-ttu-id="b234f-187">Copiez l’**URL de consommateur** et collez-la dans la zone de texte **URL de réponse** sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="b234f-187">Copy the **Consumer url** and paste it in **Reply Url** textbox on Azure portal.</span></span>
   
      <span data-ttu-id="b234f-188">d.</span><span class="sxs-lookup"><span data-stu-id="b234f-188">d.</span></span> <span data-ttu-id="b234f-189">Cliquez sur **Enregistrer** sur le portail Azure pour enregistrer les modifications.</span><span class="sxs-lookup"><span data-stu-id="b234f-189">Click **Save** on Azure portal to save the changes.</span></span>      

12. <span data-ttu-id="b234f-190">Cliquez sur **Configurer les paramètres du fournisseur d’identité** pour ouvrir la boîte de dialogue **Modifier les paramètres du fournisseur d’identité**.</span><span class="sxs-lookup"><span data-stu-id="b234f-190">Click **Configure IdP Settings** to open **Edit IdP Settings** dialog.</span></span> <span data-ttu-id="b234f-191">Cliquez sur **Choisir un fichier** pour trouver le fichier **Metadata.xml** que vous avez enregistré depuis le portail, puis chargez-le.</span><span class="sxs-lookup"><span data-stu-id="b234f-191">Click **Choose File** to locate the **Metadata.xml** file you saved from Azure portal, then upload it.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig5.png)
  
13. <span data-ttu-id="b234f-193">Cliquez sur **Save changes**.</span><span class="sxs-lookup"><span data-stu-id="b234f-193">Click **Save changes**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfigsavebutton.png)

> [!TIP]
> <span data-ttu-id="b234f-195">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="b234f-195">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b234f-196">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="b234f-196">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b234f-197">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b234f-197">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b234f-198">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="b234f-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="b234f-199">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="b234f-199">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="b234f-201">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b234f-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b234f-202">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b234f-202">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b234f-204">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="b234f-204">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b234f-206">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="b234f-206">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b234f-208">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="b234f-208">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b234f-210">a.</span><span class="sxs-lookup"><span data-stu-id="b234f-210">a.</span></span> <span data-ttu-id="b234f-211">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b234f-211">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b234f-212">b.</span><span class="sxs-lookup"><span data-stu-id="b234f-212">b.</span></span> <span data-ttu-id="b234f-213">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b234f-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b234f-214">c.</span><span class="sxs-lookup"><span data-stu-id="b234f-214">c.</span></span> <span data-ttu-id="b234f-215">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="b234f-215">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b234f-216">d.</span><span class="sxs-lookup"><span data-stu-id="b234f-216">d.</span></span> <span data-ttu-id="b234f-217">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="b234f-217">Click **Create**.</span></span>
 
### <a name="creating-a-wdesk-test-user"></a><span data-ttu-id="b234f-218">Création d’un utilisateur de test Wdesk</span><span class="sxs-lookup"><span data-stu-id="b234f-218">Creating a Wdesk test user</span></span>

<span data-ttu-id="b234f-219">Pour se connecter à Wdesk, les utilisateurs d’Azure AD doivent être approvisionnés dans Wdesk.</span><span class="sxs-lookup"><span data-stu-id="b234f-219">To enable Azure AD users to log in to Wdesk, they must be provisioned into Wdesk.</span></span> <span data-ttu-id="b234f-220">Dans Wdesk, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="b234f-220">In Wdesk, provisioning is a manual task.</span></span>

<span data-ttu-id="b234f-221">**Pour approvisionner un compte d’utilisateur, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b234f-221">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="b234f-222">Connectez-vous à Wdesk en tant qu’administrateur de la sécurité.</span><span class="sxs-lookup"><span data-stu-id="b234f-222">Log in to Wdesk as a Security Administrator.</span></span>
2. <span data-ttu-id="b234f-223">Accédez à **Administrateur** > **Compte Administrateur**.</span><span class="sxs-lookup"><span data-stu-id="b234f-223">Navigate to **Admin** > **Account Admin**.</span></span>

     ![Configurer l’authentification unique](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

3. <span data-ttu-id="b234f-225">Dans **Personnes**, cliquez sur **Membres**.</span><span class="sxs-lookup"><span data-stu-id="b234f-225">Click **Members** under **People**.</span></span>

4. <span data-ttu-id="b234f-226">Cliquez maintenant sur **Ajouter membre** pour ouvrir la boîte de dialogue **Ajouter membre**.</span><span class="sxs-lookup"><span data-stu-id="b234f-226">Now click **Add Member** to open **Add Member** dialog box.</span></span> 
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser1.png)  

5. <span data-ttu-id="b234f-228">Dans la zone de texte **Utilisateur**, entrez un nom d’utilisateur, par exemple **brittasimon@contoso.com**, puis cliquez sur **Continuer**.</span><span class="sxs-lookup"><span data-stu-id="b234f-228">In **User** text box, enter the username of user like **brittasimon@contoso.com** and click **Continue** button.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser3.png)

6.  <span data-ttu-id="b234f-230">Renseignez les détails comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="b234f-230">Enter the details as shown below:</span></span>
  
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser4.png)
 
    <span data-ttu-id="b234f-232">a.</span><span class="sxs-lookup"><span data-stu-id="b234f-232">a.</span></span> <span data-ttu-id="b234f-233">Dans la zone de texte **E-mail**, entrez une adresse e-mail d’utilisateur, par exemple **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="b234f-233">In **E-mail** text box, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="b234f-234">b.</span><span class="sxs-lookup"><span data-stu-id="b234f-234">b.</span></span> <span data-ttu-id="b234f-235">Dans la zone de texte **Prénom**, entrez le prénom de l’utilisateur, par exemple **Britta**.</span><span class="sxs-lookup"><span data-stu-id="b234f-235">In **First Name** text box, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="b234f-236">c.</span><span class="sxs-lookup"><span data-stu-id="b234f-236">c.</span></span> <span data-ttu-id="b234f-237">Dans la zone de texte **Nom**, entrez le nom de l’utilisateur, par exemple **Simon**.</span><span class="sxs-lookup"><span data-stu-id="b234f-237">In **Last Name** text box, enter the last name of user like **Simon**.</span></span>

7. <span data-ttu-id="b234f-238">Cliquez sur **Enregistrer membre**.</span><span class="sxs-lookup"><span data-stu-id="b234f-238">Click **Save Member** button.</span></span>  

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wdesk-tutorial/createuser5.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b234f-240">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="b234f-240">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b234f-241">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Wdesk.</span><span class="sxs-lookup"><span data-stu-id="b234f-241">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Wdesk.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="b234f-243">**Pour affecter Britta Simon à Wdesk, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b234f-243">**To assign Britta Simon to Wdesk, perform the following steps:**</span></span>

1. <span data-ttu-id="b234f-244">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="b234f-244">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="b234f-246">Dans la liste des applications, sélectionnez **Wdesk**.</span><span class="sxs-lookup"><span data-stu-id="b234f-246">In the applications list, select **Wdesk**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-wdesk-tutorial/tutorial_wdesk_app.png) 

3. <span data-ttu-id="b234f-248">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="b234f-248">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="b234f-250">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="b234f-250">Click **Add** button.</span></span> <span data-ttu-id="b234f-251">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="b234f-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="b234f-253">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="b234f-253">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b234f-254">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="b234f-254">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b234f-255">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="b234f-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b234f-256">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="b234f-256">Testing single sign-on</span></span>

<span data-ttu-id="b234f-257">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="b234f-257">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b234f-258">Lorsque vous cliquez sur la vignette Wdesk dans le volet d’accès, vous êtes connecté automatiquement à votre application Wdesk.</span><span class="sxs-lookup"><span data-stu-id="b234f-258">When you click the Wdesk tile in the Access Panel, you should get automatically signed-on to your Wdesk application.</span></span>
<span data-ttu-id="b234f-259">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b234f-259">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="b234f-260">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="b234f-260">Additional resources</span></span>

* [<span data-ttu-id="b234f-261">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b234f-261">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b234f-262">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="b234f-262">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wdesk-tutorial/tutorial_general_203.png

