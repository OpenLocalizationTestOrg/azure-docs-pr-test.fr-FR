---
title: "Didacticiel : Intégration d'Azure Active Directory avec Datahug | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Datahug."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5c0dc1ea-7ff4-4554-b60b-0f2fa9f5abaa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/18/2017
ms.author: jeedes
ms.openlocfilehash: ec431dd5ccfa53e4b975e46da247704dd1e15c2c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-datahug"></a><span data-ttu-id="297f0-103">Didacticiel : Intégration d’Azure Active Directory avec Datahug</span><span class="sxs-lookup"><span data-stu-id="297f0-103">Tutorial: Azure Active Directory integration with Datahug</span></span>

<span data-ttu-id="297f0-104">Dans ce didacticiel, vous allez apprendre à intégrer Datahug avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="297f0-104">In this tutorial, you learn how to integrate Datahug with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="297f0-105">L’intégration de Datahug avec Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="297f0-105">Integrating Datahug with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="297f0-106">Dans Azure AD, vous pouvez contrôler qui a accès à Datahug.</span><span class="sxs-lookup"><span data-stu-id="297f0-106">You can control in Azure AD who has access to Datahug</span></span>
- <span data-ttu-id="297f0-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Datahug (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="297f0-107">You can enable your users to automatically get signed-on to Datahug (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="297f0-108">Vous pouvez gérer vos comptes dans un emplacement central : le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="297f0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="297f0-109">Pour en savoir plus sur l’intégration de l’application SaaS avec Azure AD, consultez</span><span class="sxs-lookup"><span data-stu-id="297f0-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="297f0-110">[Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="297f0-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="297f0-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="297f0-111">Prerequisites</span></span>

<span data-ttu-id="297f0-112">Pour configurer l’intégration d’Azure AD avec Datahug, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="297f0-112">To configure Azure AD integration with Datahug, you need the following items:</span></span>

- <span data-ttu-id="297f0-113">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="297f0-113">An Azure AD subscription</span></span>
- <span data-ttu-id="297f0-114">Un abonnement Datahug pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="297f0-114">A Datahug single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="297f0-115">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="297f0-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="297f0-116">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="297f0-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="297f0-117">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="297f0-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="297f0-118">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="297f0-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="297f0-119">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="297f0-119">Scenario description</span></span>
<span data-ttu-id="297f0-120">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="297f0-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="297f0-121">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="297f0-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="297f0-122">Ajout de Datahug depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="297f0-122">Adding Datahug from the gallery</span></span>
2. <span data-ttu-id="297f0-123">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="297f0-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-datahug-from-the-gallery"></a><span data-ttu-id="297f0-124">Ajout de Datahug depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="297f0-124">Adding Datahug from the gallery</span></span>
<span data-ttu-id="297f0-125">Pour configurer l’intégration de Datahug dans Azure AD, vous devez ajouter Datahug à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="297f0-125">To configure the integration of Datahug into Azure AD, you need to add Datahug from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="297f0-126">**Pour ajouter Datahug à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="297f0-126">**To add Datahug from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="297f0-127">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="297f0-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="297f0-129">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="297f0-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="297f0-130">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="297f0-130">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="297f0-132">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="297f0-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="297f0-134">Dans la zone de recherche, tapez **Datahug**.</span><span class="sxs-lookup"><span data-stu-id="297f0-134">In the search box, type **Datahug**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_search.png)

5. <span data-ttu-id="297f0-136">Dans le volet de résultats, sélectionnez **Datahug**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="297f0-136">In the results panel, select **Datahug**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="297f0-138">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="297f0-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="297f0-139">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Datahug, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="297f0-139">In this section, you configure and test Azure AD single sign-on with Datahug based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="297f0-140">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Datahug correspondant dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="297f0-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Datahug is to a user in Azure AD.</span></span> <span data-ttu-id="297f0-141">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Datahug associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="297f0-141">In other words, a link relationship between an Azure AD user and the related user in Datahug needs to be established.</span></span>

<span data-ttu-id="297f0-142">Pour ce faire, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **Nom d’utilisateur** dans Datahug.</span><span class="sxs-lookup"><span data-stu-id="297f0-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Datahug.</span></span>

<span data-ttu-id="297f0-143">Pour configurer et tester l’authentification unique Azure AD avec Datahug, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="297f0-143">To configure and test Azure AD single sign-on with Datahug, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="297f0-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="297f0-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="297f0-145">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="297f0-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="297f0-146">**[Création d'un utilisateur test Datahug](#creating-a-datahug-test-user)** pour avoir un équivalent de Britta Simon dans Datahug lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="297f0-146">**[Creating a Datahug test user](#creating-a-datahug-test-user)** - to have a counterpart of Britta Simon in Datahug that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="297f0-147">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="297f0-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="297f0-148">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="297f0-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="297f0-149">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="297f0-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="297f0-150">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Datahug.</span><span class="sxs-lookup"><span data-stu-id="297f0-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Datahug application.</span></span>

<span data-ttu-id="297f0-151">**Pour configurer l’authentification unique Azure AD avec Datahug, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="297f0-151">**To configure Azure AD single sign-on with Datahug, perform the following steps:**</span></span>

1. <span data-ttu-id="297f0-152">Dans le Portail Azure, sur la page d’intégration de l’application **Datahug**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="297f0-152">In the Azure portal, on the **Datahug** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="297f0-154">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="297f0-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_samlbase.png)

3. <span data-ttu-id="297f0-156">Dans la section **Domaines et URL Datahug**, si vous souhaitez configurer l’application en mode initié par **IDP**, suivez les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="297f0-156">On the **Datahug Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_ur1.png)

    <span data-ttu-id="297f0-158">a.</span><span class="sxs-lookup"><span data-stu-id="297f0-158">a.</span></span> <span data-ttu-id="297f0-159">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://apps.datahug.com/identity/<uniqueID>`</span><span class="sxs-lookup"><span data-stu-id="297f0-159">In the **Identifier** textbox, type a URL using the following pattern: `https://apps.datahug.com/identity/<uniqueID>`</span></span>

    <span data-ttu-id="297f0-160">b.</span><span class="sxs-lookup"><span data-stu-id="297f0-160">b.</span></span> <span data-ttu-id="297f0-161">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://apps.datahug.com/identity/<uniqueID>/acs`</span><span class="sxs-lookup"><span data-stu-id="297f0-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://apps.datahug.com/identity/<uniqueID>/acs`</span></span>

4. <span data-ttu-id="297f0-162">Cliquez sur **Afficher les paramètres d’URL avancés**.</span><span class="sxs-lookup"><span data-stu-id="297f0-162">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="297f0-163">Si vous souhaitez configurer l’application en mode initié par le **fournisseur de service** :</span><span class="sxs-lookup"><span data-stu-id="297f0-163">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_url2.png)

    <span data-ttu-id="297f0-165">Dans la zone de texte **URL d’authentification**, tapez l’URL : `https://apps.datahug.com/`</span><span class="sxs-lookup"><span data-stu-id="297f0-165">In the **Sign-on URL** textbox, type a URL as: `https://apps.datahug.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="297f0-166">Il ne s’agit pas des valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="297f0-166">These values are not the real.</span></span> <span data-ttu-id="297f0-167">Mettez à jour ces valeurs avec l’identificateur et l’URL de réponse réels.</span><span class="sxs-lookup"><span data-stu-id="297f0-167">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="297f0-168">Nous vous suggérons d’utiliser ici la valeur de chaîne unique dans l’identificateur et l’URL de réponse.</span><span class="sxs-lookup"><span data-stu-id="297f0-168">Here we suggest you to use the unique value of string in the Identifier and Reply URL.</span></span> <span data-ttu-id="297f0-169">Pour obtenir ces valeurs, contactez l’[équipe de support technique Datahug](http://datahug.com/about/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="297f0-169">Contact [Datahug Client support team](http://datahug.com/about/contact-us/) to get these values.</span></span> 

5. <span data-ttu-id="297f0-170">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="297f0-170">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_certificate.png) 

6.  <span data-ttu-id="297f0-172">Vérifiez **« Afficher les paramètres avancés de signature de certificat »** et procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="297f0-172">Check **“Show advanced certificate signing settings”** and perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_cert.png)

    <span data-ttu-id="297f0-174">a.</span><span class="sxs-lookup"><span data-stu-id="297f0-174">a.</span></span> <span data-ttu-id="297f0-175">Dans **Option de signature**, sélectionnez **Signer l’assertion SAML**.</span><span class="sxs-lookup"><span data-stu-id="297f0-175">In **Signing Option**, select **Sign SAML assertion**.</span></span>
    
    <span data-ttu-id="297f0-176">b.</span><span class="sxs-lookup"><span data-stu-id="297f0-176">b.</span></span> <span data-ttu-id="297f0-177">Dans **Algorithme de signature**, sélectionnez **SHA1**.</span><span class="sxs-lookup"><span data-stu-id="297f0-177">In **Signing algorithm**, select **SHA1**.</span></span>
 
7. <span data-ttu-id="297f0-178">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="297f0-178">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-datahug-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="297f0-180">Dans la section **Configuration de Datahug** , cliquez sur **Configurer Datahug** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="297f0-180">On the **Datahug Configuration** section, click **Configure Datahug** to open **Configure sign-on** window.</span></span> <span data-ttu-id="297f0-181">Copiez **l’ID d’entité SAML** et **l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="297f0-181">Copy the **SAML Entity ID** and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_configure.png) 

9. <span data-ttu-id="297f0-183">Pour configurer l’authentification unique côté **Datahug**, vous devez envoyer le **XML de métadonnées**, **l’ID d’entité SAML** et **l’URL du service d’authentification unique SAML** téléchargés à [l’équipe de support Datahug](http://datahug.com/about/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="297f0-183">To configure single sign-on on **Datahug** side, you need to send the downloaded **Metadata XML**, **SAML Entity ID** and **SAML Single Sign-On Service URL** to [Datahug support](http://datahug.com/about/contact-us/).</span></span> <span data-ttu-id="297f0-184">Ils effectuent les réglages nécessaires sur l’application pour que la connexion SSO SAML soit définie correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="297f0-184">They set this application up to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="297f0-185">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="297f0-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="297f0-186">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="297f0-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="297f0-187">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="297f0-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="297f0-188">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="297f0-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="297f0-189">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="297f0-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="297f0-191">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="297f0-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="297f0-192">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="297f0-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-datahug-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="297f0-194">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="297f0-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-datahug-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="297f0-196">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="297f0-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-datahug-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="297f0-198">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="297f0-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-datahug-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="297f0-200">a.</span><span class="sxs-lookup"><span data-stu-id="297f0-200">a.</span></span> <span data-ttu-id="297f0-201">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="297f0-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="297f0-202">b.</span><span class="sxs-lookup"><span data-stu-id="297f0-202">b.</span></span> <span data-ttu-id="297f0-203">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="297f0-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="297f0-204">c.</span><span class="sxs-lookup"><span data-stu-id="297f0-204">c.</span></span> <span data-ttu-id="297f0-205">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="297f0-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="297f0-206">d.</span><span class="sxs-lookup"><span data-stu-id="297f0-206">d.</span></span> <span data-ttu-id="297f0-207">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="297f0-207">Click **Create**.</span></span>
 
### <a name="creating-a-datahug-test-user"></a><span data-ttu-id="297f0-208">Création d’un utilisateur de test Datahug</span><span class="sxs-lookup"><span data-stu-id="297f0-208">Creating a Datahug test user</span></span>

<span data-ttu-id="297f0-209">Pour se connecter à Datahug, les utilisateurs d’Azure AD doivent être approvisionnés dans Datahug.</span><span class="sxs-lookup"><span data-stu-id="297f0-209">To enable Azure AD users to log in to Datahug, they must be provisioned into Datahug.</span></span>  
<span data-ttu-id="297f0-210">Pour Datahug, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="297f0-210">When Datahug, provisioning is a manual task.</span></span>

<span data-ttu-id="297f0-211">**Pour approvisionner un compte d’utilisateur, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="297f0-211">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="297f0-212">Connectez-vous à votre site d’entreprise Datahug en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="297f0-212">Log in to your Datahug company site as an administrator.</span></span>

2. <span data-ttu-id="297f0-213">Passez la souris sur la **roue dentée** dans le coin supérieur droit et cliquez sur **Paramètres**</span><span class="sxs-lookup"><span data-stu-id="297f0-213">Hover over the **cog** in the top right-hand corner and click **Settings**</span></span>
   
   ![Ajouter un employé](./media/active-directory-saas-datahug-tutorial/1.png)

3. <span data-ttu-id="297f0-215">Choisissez **People** (Personnes) et cliquez sur l’onglet **Ajouter des utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="297f0-215">Choose **People** and click the **Add Users** tab</span></span>

    ![Ajouter un employé](./media/active-directory-saas-datahug-tutorial/2.png)

4. <span data-ttu-id="297f0-217">Tapez l’adresse électronique de la personne pour laquelle vous souhaitez créer un compte et cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="297f0-217">Type the email of the person you would like to create an account for and click **Add**.</span></span>

    ![Ajouter un employé](./media/active-directory-saas-datahug-tutorial/3.png)

    > [!NOTE] 
    > <span data-ttu-id="297f0-219">Vous pouvez envoyer un courrier d’inscription à l’utilisateur en sélectionnant **Send welcome email** (Envoyer un e-mail de bienvenue).</span><span class="sxs-lookup"><span data-stu-id="297f0-219">You can send registration mail to user by selecting **Send welcome email** checkbox.</span></span>  
    > <span data-ttu-id="297f0-220">Si vous créez un compte pour l’équipe commerciale, n’envoyez pas l’e-mail de bienvenue.</span><span class="sxs-lookup"><span data-stu-id="297f0-220">If you are creating an account for Salesforce do not send the welcome email.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="297f0-221">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="297f0-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="297f0-222">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Datahug.</span><span class="sxs-lookup"><span data-stu-id="297f0-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Datahug.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="297f0-224">**Pour affecter Britta Simon à Datahug, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="297f0-224">**To assign Britta Simon to Datahug, perform the following steps:**</span></span>

1. <span data-ttu-id="297f0-225">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="297f0-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="297f0-227">Dans la liste des applications, sélectionnez **Datahug**.</span><span class="sxs-lookup"><span data-stu-id="297f0-227">In the applications list, select **Datahug**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_app.png) 

3. <span data-ttu-id="297f0-229">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="297f0-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="297f0-231">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="297f0-231">Click **Add** button.</span></span> <span data-ttu-id="297f0-232">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="297f0-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="297f0-234">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="297f0-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="297f0-235">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="297f0-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="297f0-236">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="297f0-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="297f0-237">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="297f0-237">Testing single sign-on</span></span>

<span data-ttu-id="297f0-238">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="297f0-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
<span data-ttu-id="297f0-239">Lorsque vous cliquez sur la vignette Datahug dans le volet d’accès, vous êtes automatiquement connecté à votre application Datahug.</span><span class="sxs-lookup"><span data-stu-id="297f0-239">When you click the Datahug tile in the Access Panel, you should get automatically signed-on to your Datahug application.</span></span> <span data-ttu-id="297f0-240">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="297f0-240">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="297f0-241">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="297f0-241">Additional resources</span></span>

* [<span data-ttu-id="297f0-242">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="297f0-242">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="297f0-243">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="297f0-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_203.png

