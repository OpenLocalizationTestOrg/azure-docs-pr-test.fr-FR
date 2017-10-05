---
title: "Didacticiel : Intégration d’Azure Active Directory à YouEarnedIt | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et YouEarnedIt."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3011d44d-dfcf-4061-888f-cff90fbc8150
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: jeedes
ms.openlocfilehash: c29d218dbca581f102caf8070fa40894e7006e71
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-youearnedit"></a><span data-ttu-id="b08b7-103">Didacticiel : Intégration d’Azure Active Directory à YouEarnedIt</span><span class="sxs-lookup"><span data-stu-id="b08b7-103">Tutorial: Azure Active Directory integration with YouEarnedIt</span></span>

<span data-ttu-id="b08b7-104">Dans ce didacticiel, vous allez apprendre à intégrer YouEarnedIt à Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="b08b7-104">In this tutorial, you learn how to integrate YouEarnedIt with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b08b7-105">L’intégration d’YouEarnedIt à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="b08b7-105">Integrating YouEarnedIt with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b08b7-106">Dans Azure AD, vous pouvez contrôler qui a accès à YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="b08b7-106">You can control in Azure AD who has access to YouEarnedIt.</span></span>
- <span data-ttu-id="b08b7-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à YouEarnedIt (par le biais de l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b08b7-107">You can enable your users to automatically get signed-on to YouEarnedIt (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="b08b7-108">Vous pouvez gérer vos comptes dans un emplacement central : le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="b08b7-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="b08b7-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b08b7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b08b7-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b08b7-110">Prerequisites</span></span>

<span data-ttu-id="b08b7-111">Pour configurer l’intégration de YouEarnedIt à Azure AD, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="b08b7-111">To configure Azure AD integration with YouEarnedIt, you need the following items:</span></span>

- <span data-ttu-id="b08b7-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="b08b7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b08b7-113">Un abonnement YouEarnedIt pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="b08b7-113">A YouEarnedIt single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b08b7-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="b08b7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b08b7-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="b08b7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b08b7-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="b08b7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b08b7-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b08b7-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b08b7-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="b08b7-118">Scenario description</span></span>
<span data-ttu-id="b08b7-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="b08b7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b08b7-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="b08b7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b08b7-121">Ajout d’YouEarnedIt depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="b08b7-121">Adding YouEarnedIt from the gallery</span></span>
2. <span data-ttu-id="b08b7-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b08b7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-youearnedit-from-the-gallery"></a><span data-ttu-id="b08b7-123">Ajout d’YouEarnedIt depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="b08b7-123">Adding YouEarnedIt from the gallery</span></span>
<span data-ttu-id="b08b7-124">Pour configurer l’intégration de YouEarnedIt à Azure AD, vous devez ajouter YouEarnedIt à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="b08b7-124">To configure the integration of YouEarnedIt into Azure AD, you need to add YouEarnedIt from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b08b7-125">**Pour ajouter YouEarnedIt à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b08b7-125">**To add YouEarnedIt from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b08b7-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b08b7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Bouton Azure Active Directory][1]

2. <span data-ttu-id="b08b7-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="b08b7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b08b7-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="b08b7-129">Then go to **All applications**.</span></span>

    ![Panneau Applications d’entreprise][2]
    
3. <span data-ttu-id="b08b7-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="b08b7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Bouton Nouvelle application][3]

4. <span data-ttu-id="b08b7-133">Dans la zone de recherche, tapez **YouEarnedIt**, sélectionnez **YouEarnedIt** dans le panneau de résultats, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="b08b7-133">In the search box, type **YouEarnedt**, select  **YouEarnedt**  from result panel then click **Add** button to add the application.</span></span>

    ![YouEarnedIt dans la liste des résultats](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b08b7-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b08b7-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="b08b7-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec YouEarnedIt avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="b08b7-136">In this section, you configure and test Azure AD single sign-on with YouEarnedIt based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b08b7-137">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur YouEarnedIt équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b08b7-137">For single sign-on to work, Azure AD needs to know what the counterpart user in YouEarnedIt is to a user in Azure AD.</span></span> <span data-ttu-id="b08b7-138">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur YouEarnedIt associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="b08b7-138">In other words, a link relationship between an Azure AD user and the related user in YouEarnedIt needs to be established.</span></span>

<span data-ttu-id="b08b7-139">Dans YouEarnedIt, assignez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="b08b7-139">In YouEarnedIt, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b08b7-140">Pour configurer et tester l’authentification unique Azure AD avec YouEarnedIt, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="b08b7-140">To configure and test Azure AD single sign-on with YouEarnedIt, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b08b7-141">**[Configurer l’authentification unique Azure AD](#configure-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="b08b7-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b08b7-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b08b7-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b08b7-143">**[Créer un utilisateur de test YouEarnedIt](#create-a-youearnedit-test-user)** pour avoir un équivalent de Britta Simon dans YouEarnedIt lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b08b7-143">**[Create a YouEarnedIt test user](#create-a-youearnedit-test-user)** - to have a counterpart of Britta Simon in YouEarnedIt that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b08b7-144">**[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b08b7-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b08b7-145">**[Tester l’authentification unique](#test-single-sign-on)** : pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="b08b7-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b08b7-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b08b7-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b08b7-147">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="b08b7-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your YouEarnedIt application.</span></span>

<span data-ttu-id="b08b7-148">**Pour configurer l’authentification unique Azure AD avec YouEarnedIt, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b08b7-148">**To configure Azure AD single sign-on with YouEarnedIt, perform the following steps:**</span></span>

1. <span data-ttu-id="b08b7-149">Dans le portail Azure, sur la page d’intégration de l’application **YouEarnedIt**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="b08b7-149">In the Azure portal, on the **YouEarnedIt** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="b08b7-151">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="b08b7-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_samlbase.png)

3. <span data-ttu-id="b08b7-153">Dans la section **Domaine et URL YouEarnedIt**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="b08b7-153">On the **YouEarnedIt Domain and URLs** section, perform the following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL YouEarnedIt](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_url.png)

    <span data-ttu-id="b08b7-155">a.</span><span class="sxs-lookup"><span data-stu-id="b08b7-155">a.</span></span> <span data-ttu-id="b08b7-156">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant :</span><span class="sxs-lookup"><span data-stu-id="b08b7-156">In the **Sign-on URL** textbox, type a URL using the following patterns:</span></span> 
    | <span data-ttu-id="b08b7-157">Environnement</span><span class="sxs-lookup"><span data-stu-id="b08b7-157">Environment</span></span>  | <span data-ttu-id="b08b7-158">Modèle</span><span class="sxs-lookup"><span data-stu-id="b08b7-158">Pattern</span></span>  |
    |:--- |:--- |
    | <span data-ttu-id="b08b7-159">Production</span><span class="sxs-lookup"><span data-stu-id="b08b7-159">Production</span></span> | `https://<company name>.youearnedit.com/users/sign_in` |
    | <span data-ttu-id="b08b7-160">Bac à sable</span><span class="sxs-lookup"><span data-stu-id="b08b7-160">Sandbox</span></span>  |`https://<company name>.sandbox.youearnedit.com/users/sign_in` |

    <span data-ttu-id="b08b7-161">b.</span><span class="sxs-lookup"><span data-stu-id="b08b7-161">b.</span></span> <span data-ttu-id="b08b7-162">Dans la zone de texte **Identificateur**, tapez une URL au format suivant :</span><span class="sxs-lookup"><span data-stu-id="b08b7-162">In the **Identifier** textbox, type a URL using the following patterns:</span></span>
    | <span data-ttu-id="b08b7-163">Environnement</span><span class="sxs-lookup"><span data-stu-id="b08b7-163">Environment</span></span>  | <span data-ttu-id="b08b7-164">Modèle</span><span class="sxs-lookup"><span data-stu-id="b08b7-164">Pattern</span></span>  |
    |:--- |:--- |
    | <span data-ttu-id="b08b7-165">Production</span><span class="sxs-lookup"><span data-stu-id="b08b7-165">Production</span></span> | `https://<company name>.youearnedit.com` |
    | <span data-ttu-id="b08b7-166">Bac à sable</span><span class="sxs-lookup"><span data-stu-id="b08b7-166">Sandbox</span></span>  |`https://<company name>.sandbox.youearnedit.com` |

    > [!NOTE] 
    > <span data-ttu-id="b08b7-167">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="b08b7-167">These values are not real.</span></span> <span data-ttu-id="b08b7-168">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="b08b7-168">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="b08b7-169">Pour obtenir ces valeurs, contactez l’[équipe de support technique YouEarnedIt](https://youearnedit.freshdesk.com/support/tickets/new).</span><span class="sxs-lookup"><span data-stu-id="b08b7-169">Contact [YouEarnedIt Client support team](https://youearnedit.freshdesk.com/support/tickets/new) to get these values.</span></span> 
 
4. <span data-ttu-id="b08b7-170">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="b08b7-170">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Lien de téléchargement du certificat](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_certificate.png) 

5. <span data-ttu-id="b08b7-172">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="b08b7-172">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-youearnedit-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b08b7-174">Dans la section **Configuration de YouEarnedIt**, cliquez sur **Configurer YouEarnedIt** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="b08b7-174">On the **YouEarnedIt Configuration** section, click **Configure YouEarnedIt** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b08b7-175">Copiez l**’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="b08b7-175">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configuration de YouEarnedIt](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_configure.png) 

7. <span data-ttu-id="b08b7-177">Pour configurer l’authentification unique côté **YouEarnedIt**, vous devez envoyer le **Certificat (Base64)** téléchargé et **l’URL du service d’authentification unique SAML** à [l’équipe de support technique YouEarnedIt](https://youearnedit.freshdesk.com/support/tickets/new).</span><span class="sxs-lookup"><span data-stu-id="b08b7-177">To configure single sign-on on **YouEarnedIt** side, you need to send the downloaded **Certificate(Base64)** and **SAML Single Sign-On Service URL** to [YouEarnedIt support team](https://youearnedit.freshdesk.com/support/tickets/new).</span></span> <span data-ttu-id="b08b7-178">Celles-ci configurent ensuite ce paramètre pour que la connexion SSO SAML soit définie correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="b08b7-178">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="b08b7-179">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="b08b7-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b08b7-180">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="b08b7-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b08b7-181">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b08b7-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b08b7-182">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="b08b7-182">Create an Azure AD test user</span></span>

<span data-ttu-id="b08b7-183">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="b08b7-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="b08b7-185">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b08b7-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b08b7-186">Dans le volet gauche du Portail Azure, cliquez sur le bouton **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b08b7-186">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Bouton Azure Active Directory](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="b08b7-188">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="b08b7-188">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Liens « Utilisateurs et groupes » et « Tous les utilisateurs »](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="b08b7-190">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="b08b7-190">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Bouton Ajouter](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="b08b7-192">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="b08b7-192">In the **User** dialog box, perform the following steps:</span></span>

    ![Boîte de dialogue Utilisateur](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_04.png)

    <span data-ttu-id="b08b7-194">a.</span><span class="sxs-lookup"><span data-stu-id="b08b7-194">a.</span></span> <span data-ttu-id="b08b7-195">Dans la zone **Nom**, tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b08b7-195">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b08b7-196">b.</span><span class="sxs-lookup"><span data-stu-id="b08b7-196">b.</span></span> <span data-ttu-id="b08b7-197">Dans la zone **Nom d’utilisateur** , tapez l’adresse e-mail de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b08b7-197">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="b08b7-198">c.</span><span class="sxs-lookup"><span data-stu-id="b08b7-198">c.</span></span> <span data-ttu-id="b08b7-199">Cochez la case **Afficher le mot de passe**, puis notez la valeur affichée dans le champ **Mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="b08b7-199">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="b08b7-200">d.</span><span class="sxs-lookup"><span data-stu-id="b08b7-200">d.</span></span> <span data-ttu-id="b08b7-201">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="b08b7-201">Click **Create**.</span></span>
 
### <a name="create-a-youearnedit-test-user"></a><span data-ttu-id="b08b7-202">Créer un utilisateur de test YouEarnedIt</span><span class="sxs-lookup"><span data-stu-id="b08b7-202">Create a YouEarnedIt test user</span></span>

<span data-ttu-id="b08b7-203">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="b08b7-203">In this section, you create a user called Britta Simon in YouEarnedIt.</span></span> <span data-ttu-id="b08b7-204">Collaborez avec l’équipe du support technique YouEarnedIt pour ajouter des utilisateurs dans YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="b08b7-204">Please work with YouEarnedIt support team to add the users in the YouEarnedIt platform.</span></span>

>[!NOTE]
><span data-ttu-id="b08b7-205">YouEarnedIt attend du fournisseur d'identité qu’il fournisse une valeur de nom d’utilisateur ou d’adresse e-mail dans l’attribut NameID.</span><span class="sxs-lookup"><span data-stu-id="b08b7-205">YouEarnedIt expect the Identity Provider to supply an EmailAddress  or UserName in the NameID attribute.</span></span> <span data-ttu-id="b08b7-206">L’authentification échoue si aucune valeur de nom d’utilisateur ou d’adresse e-mail n’est trouvée dans la base de données ou ne correspond exactement.</span><span class="sxs-lookup"><span data-stu-id="b08b7-206">Authentication will fail if a corresponding UserName or EmailAddress is not found within the database or does not match exactly.</span></span> <span data-ttu-id="b08b7-207">Cette opération nécessite l’importation des comptes dans le système de YouEarnedIt avant l’intégration de l’authentification unique (en général, via l’importation CSV ou API).</span><span class="sxs-lookup"><span data-stu-id="b08b7-207">This will require that accounts be imported into the YouEarnedIt system before the SSO integration (Typically either via API or CSV import).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="b08b7-208">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="b08b7-208">Assign the Azure AD test user</span></span>

<span data-ttu-id="b08b7-209">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="b08b7-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to YouEarnedIt.</span></span>

![Attribuer le rôle d’utilisateur][200] 

<span data-ttu-id="b08b7-211">**Pour affecter Britta Simon à YouEarnedIt, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b08b7-211">**To assign Britta Simon to YouEarnedIt, perform the following steps:**</span></span>

1. <span data-ttu-id="b08b7-212">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="b08b7-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="b08b7-214">Dans la liste des applications, sélectionnez **YouEarnedIt**.</span><span class="sxs-lookup"><span data-stu-id="b08b7-214">In the applications list, select **YouEarnedIt**.</span></span>

    ![Lien YouEarnedIt dans la liste des applications](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_app.png)  

3. <span data-ttu-id="b08b7-216">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="b08b7-216">In the menu on the left, click **Users and groups**.</span></span>

    ![Lien « Utilisateurs et groupes »][202]

4. <span data-ttu-id="b08b7-218">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="b08b7-218">Click **Add** button.</span></span> <span data-ttu-id="b08b7-219">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="b08b7-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Volet Ajouter une attribution][203]

5. <span data-ttu-id="b08b7-221">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="b08b7-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b08b7-222">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="b08b7-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b08b7-223">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="b08b7-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b08b7-224">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="b08b7-224">Test single sign-on</span></span>

<span data-ttu-id="b08b7-225">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="b08b7-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b08b7-226">Quand vous cliquez sur la vignette YouEarnedIt dans le volet d’accès, vous devez être connecté automatiquement à votre application YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="b08b7-226">When you click the YouEarnedIt tile in the Access Panel, you should get automatically signed-on to your YouEarnedIt application.</span></span>
<span data-ttu-id="b08b7-227">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b08b7-227">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b08b7-228">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="b08b7-228">Additional resources</span></span>

* [<span data-ttu-id="b08b7-229">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b08b7-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b08b7-230">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="b08b7-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_203.png

