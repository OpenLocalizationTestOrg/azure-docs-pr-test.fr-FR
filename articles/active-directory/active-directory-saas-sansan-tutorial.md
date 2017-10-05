---
title: "Didacticiel : Intégration d’Azure Active Directory avec SanSan | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et SanSan."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f653a0f2-c44a-4670-b936-68c136b578ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: e1a9653d5feea910308cefabdbdfe3a6af44bbe4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sansan"></a><span data-ttu-id="a9c56-103">Didacticiel : Intégration d’Azure Active Directory avec SanSan</span><span class="sxs-lookup"><span data-stu-id="a9c56-103">Tutorial: Azure Active Directory integration with Sansan</span></span>

<span data-ttu-id="a9c56-104">Dans ce didacticiel, vous allez apprendre à intégrer SanSan avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a9c56-104">In this tutorial, you learn how to integrate Sansan with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a9c56-105">L’intégration de SanSan avec Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="a9c56-105">Integrating Sansan with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a9c56-106">Vous pouvez contrôler dans Azure AD qui a accès à SanSan.</span><span class="sxs-lookup"><span data-stu-id="a9c56-106">You can control in Azure AD who has access to Sansan</span></span>
- <span data-ttu-id="a9c56-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à SanSan (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a9c56-107">You can enable your users to automatically get signed-on to Sansan (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a9c56-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a9c56-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a9c56-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a9c56-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a9c56-110">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="a9c56-110">Prerequisites</span></span>

<span data-ttu-id="a9c56-111">Pour configurer l’intégration d’Azure AD avec SanSan, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="a9c56-111">To configure Azure AD integration with Sansan, you need the following items:</span></span>

- <span data-ttu-id="a9c56-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="a9c56-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a9c56-113">Un abonnement SanSan pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="a9c56-113">A Sansan single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a9c56-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="a9c56-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a9c56-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="a9c56-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a9c56-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="a9c56-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a9c56-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a9c56-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a9c56-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="a9c56-118">Scenario description</span></span>
<span data-ttu-id="a9c56-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="a9c56-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a9c56-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="a9c56-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a9c56-121">Ajout de SanSan à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="a9c56-121">Adding Sansan from the gallery</span></span>
2. <span data-ttu-id="a9c56-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a9c56-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sansan-from-the-gallery"></a><span data-ttu-id="a9c56-123">Ajout de SanSan à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="a9c56-123">Adding Sansan from the gallery</span></span>
<span data-ttu-id="a9c56-124">Pour configurer l’intégration de SanSan à Azure AD, vous devez ajouter SanSan à partir de la galerie à votre liste d’applications SaaS managées.</span><span class="sxs-lookup"><span data-stu-id="a9c56-124">To configure the integration of Sansan into Azure AD, you need to add Sansan from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a9c56-125">**Pour ajouter SanSan à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a9c56-125">**To add Sansan from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a9c56-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a9c56-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a9c56-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="a9c56-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a9c56-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="a9c56-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="a9c56-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="a9c56-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="a9c56-133">Dans la zone de recherche, tapez **SanSan**.</span><span class="sxs-lookup"><span data-stu-id="a9c56-133">In the search box, type **Sansan**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_search.png)

5. <span data-ttu-id="a9c56-135">Dans le volet de résultats, sélectionnez **SanSan**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="a9c56-135">In the results panel, select **Sansan**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a9c56-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a9c56-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a9c56-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec SanSan sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="a9c56-138">In this section, you configure and test Azure AD single sign-on with Sansan based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a9c56-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur SanSan équivalent à l’utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a9c56-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Sansan is to a user in Azure AD.</span></span> <span data-ttu-id="a9c56-140">En d’autres termes, il faut établir une relation entre l’utilisateur Azure AD et l’utilisateur SanSan associé.</span><span class="sxs-lookup"><span data-stu-id="a9c56-140">In other words, a link relationship between an Azure AD user and the related user in Sansan needs to be established.</span></span>

<span data-ttu-id="a9c56-141">Dans SanSan, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **Username** pour établir la relation de lien.</span><span class="sxs-lookup"><span data-stu-id="a9c56-141">In Sansan, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a9c56-142">Pour configurer et tester l’authentification unique Azure AD avec SanSan, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="a9c56-142">To configure and test Azure AD single sign-on with Sansan, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a9c56-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="a9c56-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a9c56-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a9c56-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a9c56-145">**[Création d’un utilisateur de test SanSan](#creating-a-sansan-test-user)** pour avoir un équivalent de Britta Simon dans SanSan, lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="a9c56-145">**[Creating a Sansan test user](#creating-a-sansan-test-user)** - to have a counterpart of Britta Simon in Sansan that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a9c56-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a9c56-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a9c56-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="a9c56-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a9c56-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a9c56-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a9c56-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application SanSan.</span><span class="sxs-lookup"><span data-stu-id="a9c56-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Sansan application.</span></span>

<span data-ttu-id="a9c56-150">**Pour configurer l’authentification unique Azure AD avec SanSan, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a9c56-150">**To configure Azure AD single sign-on with Sansan, perform the following steps:**</span></span>

1. <span data-ttu-id="a9c56-151">Dans le portail Azure, sur la page d’intégration de l’application **SanSan**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="a9c56-151">In the Azure portal, on the **Sansan** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="a9c56-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="a9c56-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_samlbase.png)

3. <span data-ttu-id="a9c56-155">Dans la section **Domaine et URL SanSan**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="a9c56-155">On the **Sansan Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_url.png)

    <span data-ttu-id="a9c56-157">a.</span><span class="sxs-lookup"><span data-stu-id="a9c56-157">a.</span></span> <span data-ttu-id="a9c56-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant :</span><span class="sxs-lookup"><span data-stu-id="a9c56-158">In the **Sign-on URL** textbox, type a URL using the following patterns:</span></span> 
    
    | <span data-ttu-id="a9c56-159">Environnement</span><span class="sxs-lookup"><span data-stu-id="a9c56-159">Environment</span></span> | <span data-ttu-id="a9c56-160">URL</span><span class="sxs-lookup"><span data-stu-id="a9c56-160">URL</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="a9c56-161">Web PC</span><span class="sxs-lookup"><span data-stu-id="a9c56-161">PC web</span></span> |`https://ap.sansan.com/v/saml2/<company name>/acs` |
    | <span data-ttu-id="a9c56-162">Application mobile native</span><span class="sxs-lookup"><span data-stu-id="a9c56-162">Native Mobile app</span></span> |`https://internal.api.sansan.com/saml2/<company name>/acs` |
    | <span data-ttu-id="a9c56-163">Paramètres de navigateur mobile</span><span class="sxs-lookup"><span data-stu-id="a9c56-163">Mobile browser settings</span></span> |`https://ap.sansan.com/s/saml2/<company name>/acs` |  

    <span data-ttu-id="a9c56-164">b.</span><span class="sxs-lookup"><span data-stu-id="a9c56-164">b.</span></span> <span data-ttu-id="a9c56-165">Dans la zone de texte **Identificateur**, tapez une URL au format suivant :</span><span class="sxs-lookup"><span data-stu-id="a9c56-165">In the **Identifier** textbox, type a URL using the following patterns:</span></span>
    | <span data-ttu-id="a9c56-166">Environnement</span><span class="sxs-lookup"><span data-stu-id="a9c56-166">Environment</span></span>             | <span data-ttu-id="a9c56-167">URL</span><span class="sxs-lookup"><span data-stu-id="a9c56-167">URL</span></span> |
    | :-- | :-- |
    | <span data-ttu-id="a9c56-168">Web PC</span><span class="sxs-lookup"><span data-stu-id="a9c56-168">PC web</span></span>                  | `https://ap.sansan.com/v/saml2/<company name>`|
    | <span data-ttu-id="a9c56-169">Application mobile native</span><span class="sxs-lookup"><span data-stu-id="a9c56-169">Native Mobile app</span></span>       | `https://internal.api.sansan.com/saml2/<company name>` |
    | <span data-ttu-id="a9c56-170">Paramètres de navigateur mobile</span><span class="sxs-lookup"><span data-stu-id="a9c56-170">Mobile browser settings</span></span> | `https://ap.sansan.com/s/saml2/<company name>` |

    > [!NOTE] 
    > <span data-ttu-id="a9c56-171">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="a9c56-171">These values are not real.</span></span> <span data-ttu-id="a9c56-172">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="a9c56-172">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a9c56-173">Pour obtenir ces valeurs, contactez l’[équipe de support technique SanSan](https://www.sansan.com/form/contact).</span><span class="sxs-lookup"><span data-stu-id="a9c56-173">Contact [Sansan Client support team](https://www.sansan.com/form/contact) to get these values.</span></span> 

4. <span data-ttu-id="a9c56-174">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="a9c56-174">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_certificate.png) 

5. <span data-ttu-id="a9c56-176">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="a9c56-176">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sansan-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a9c56-178">Dans la section **Configuration de SanSan**, cliquez sur **Configurer SanSan** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="a9c56-178">On the **Sansan Configuration** section, click **Configure Sansan** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a9c56-179">Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="a9c56-179">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_configure.png) 

7. <span data-ttu-id="a9c56-181">Pour configurer l’authentification unique côté **SanSan**, vous devez envoyer le **Certificat**, l’**URL de déconnexion**, l’**ID d’entité SAML** et l’**URL du service d’authentification unique SAML** téléchargés à l’[équipe de support technique SanSan](https://www.sansan.com/form/contact).</span><span class="sxs-lookup"><span data-stu-id="a9c56-181">To configure single sign-on on **Sansan** side, you need to send the downloaded **Certificate**, **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** to [Sansan support team](https://www.sansan.com/form/contact).</span></span> <span data-ttu-id="a9c56-182">Celles-ci configurent ensuite ce paramètre pour que la connexion SSO SAML soit définie correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="a9c56-182">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

>[!NOTE]
><span data-ttu-id="a9c56-183">Les paramètres de navigateur PC fonctionnent également avec l’application mobile et le navigateur mobile avec Web PC.</span><span class="sxs-lookup"><span data-stu-id="a9c56-183">PC browser setting also work for Mobile app and Mobile browser along with PC web.</span></span>  

> [!TIP]
> <span data-ttu-id="a9c56-184">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="a9c56-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a9c56-185">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="a9c56-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a9c56-186">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a9c56-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a9c56-187">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="a9c56-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="a9c56-188">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a9c56-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="a9c56-190">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a9c56-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a9c56-191">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a9c56-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sansan-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a9c56-193">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="a9c56-193">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sansan-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a9c56-195">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="a9c56-195">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sansan-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a9c56-197">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="a9c56-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sansan-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a9c56-199">a.</span><span class="sxs-lookup"><span data-stu-id="a9c56-199">a.</span></span> <span data-ttu-id="a9c56-200">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a9c56-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a9c56-201">b.</span><span class="sxs-lookup"><span data-stu-id="a9c56-201">b.</span></span> <span data-ttu-id="a9c56-202">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a9c56-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a9c56-203">c.</span><span class="sxs-lookup"><span data-stu-id="a9c56-203">c.</span></span> <span data-ttu-id="a9c56-204">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="a9c56-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a9c56-205">d.</span><span class="sxs-lookup"><span data-stu-id="a9c56-205">d.</span></span> <span data-ttu-id="a9c56-206">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="a9c56-206">Click **Create**.</span></span>
 
### <a name="creating-a-sansan-test-user"></a><span data-ttu-id="a9c56-207">Création d’un utilisateur de test SanSan</span><span class="sxs-lookup"><span data-stu-id="a9c56-207">Creating a Sansan test user</span></span>

<span data-ttu-id="a9c56-208">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans SanSan.</span><span class="sxs-lookup"><span data-stu-id="a9c56-208">In this section, you create a user called Britta Simon in SanSan.</span></span> <span data-ttu-id="a9c56-209">Avant de procéder à l’authentification unique, tous les utilisateurs de SanSan doivent être approvisionnés dans cette application.</span><span class="sxs-lookup"><span data-stu-id="a9c56-209">SanSan application needs the user to be provisioned in the application before doing SSO.</span></span> 

>[!NOTE]
><span data-ttu-id="a9c56-210">Si vous avez besoin de créer un utilisateur manuellement ou un groupe d’utilisateurs, vous devez contacter l’[équipe de support technique SanSan](https://www.sansan.com/form/contact).</span><span class="sxs-lookup"><span data-stu-id="a9c56-210">If you need to create a user manually or batch of users, you need to contact the [Sansan support team](https://www.sansan.com/form/contact).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a9c56-211">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="a9c56-211">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a9c56-212">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à SanSan.</span><span class="sxs-lookup"><span data-stu-id="a9c56-212">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Sansan.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="a9c56-214">**Pour affecter Britta Simon à SanSan, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a9c56-214">**To assign Britta Simon to Sansan, perform the following steps:**</span></span>

1. <span data-ttu-id="a9c56-215">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="a9c56-215">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="a9c56-217">Dans la liste des applications, sélectionnez **SanSan**.</span><span class="sxs-lookup"><span data-stu-id="a9c56-217">In the applications list, select **Sansan**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sansan-tutorial/tutorial_sansan_app.png) 

3. <span data-ttu-id="a9c56-219">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="a9c56-219">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="a9c56-221">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="a9c56-221">Click **Add** button.</span></span> <span data-ttu-id="a9c56-222">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="a9c56-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="a9c56-224">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="a9c56-224">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a9c56-225">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="a9c56-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a9c56-226">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="a9c56-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a9c56-227">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="a9c56-227">Testing single sign-on</span></span>

<span data-ttu-id="a9c56-228">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="a9c56-228">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a9c56-229">Lorsque vous cliquez sur la vignette SanSan dans le volet d’accès, vous devez être connecté automatiquement à votre application SanSan.</span><span class="sxs-lookup"><span data-stu-id="a9c56-229">When you click the Sansan tile in the Access Panel, you should get automatically signed-on to your Sansan application.</span></span>
<span data-ttu-id="a9c56-230">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a9c56-230">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a9c56-231">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="a9c56-231">Additional resources</span></span>

* [<span data-ttu-id="a9c56-232">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a9c56-232">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a9c56-233">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="a9c56-233">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sansan-tutorial/tutorial_general_203.png

