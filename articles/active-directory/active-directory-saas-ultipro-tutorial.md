---
title: "Didacticiel : Intégration d’Azure Active Directory avec UltiPro | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et UltiPro."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: afc0f2b9-2eac-47ec-af04-65ed0fb0ca5a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: ab60bda1be7101d5bd0c51f5499a820db40375bf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ultipro"></a><span data-ttu-id="b1c78-103">Didacticiel : Intégration d’Azure Active Directory à UltiPro</span><span class="sxs-lookup"><span data-stu-id="b1c78-103">Tutorial: Azure Active Directory integration with UltiPro</span></span>

<span data-ttu-id="b1c78-104">Dans ce didacticiel, vous allez apprendre à intégrer UltiPro à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b1c78-104">In this tutorial, you learn how to integrate UltiPro with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b1c78-105">L’intégration d’UltiPro à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="b1c78-105">Integrating UltiPro with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b1c78-106">Dans Azure AD, vous pouvez contrôler qui a accès à UltiPro.</span><span class="sxs-lookup"><span data-stu-id="b1c78-106">You can control in Azure AD who has access to UltiPro</span></span>
- <span data-ttu-id="b1c78-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à UltiPro (authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b1c78-107">You can enable your users to automatically get signed-on to UltiPro (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b1c78-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="b1c78-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b1c78-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b1c78-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b1c78-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b1c78-110">Prerequisites</span></span>

<span data-ttu-id="b1c78-111">Pour configurer l’intégration d’Azure AD avec UltiPro, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="b1c78-111">To configure Azure AD integration with UltiPro, you need the following items:</span></span>

- <span data-ttu-id="b1c78-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="b1c78-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b1c78-113">Un abonnement UltiPro pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="b1c78-113">A UltiPro single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b1c78-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="b1c78-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b1c78-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="b1c78-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b1c78-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="b1c78-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b1c78-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b1c78-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b1c78-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="b1c78-118">Scenario description</span></span>
<span data-ttu-id="b1c78-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="b1c78-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b1c78-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="b1c78-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b1c78-121">Ajout d’UltiPro à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="b1c78-121">Adding UltiPro from the gallery</span></span>
2. <span data-ttu-id="b1c78-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b1c78-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ultipro-from-the-gallery"></a><span data-ttu-id="b1c78-123">Ajout d’UltiPro à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="b1c78-123">Adding UltiPro from the gallery</span></span>
<span data-ttu-id="b1c78-124">Pour configurer l’intégration d’UltiPro à Azure AD, vous devez ajouter UltiPro à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="b1c78-124">To configure the integration of UltiPro into Azure AD, you need to add UltiPro from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b1c78-125">**Pour ajouter UltiPro à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b1c78-125">**To add UltiPro from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b1c78-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b1c78-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b1c78-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="b1c78-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b1c78-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="b1c78-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="b1c78-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="b1c78-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="b1c78-133">Dans la zone de recherche, tapez **UltiPro**.</span><span class="sxs-lookup"><span data-stu-id="b1c78-133">In the search box, type **UltiPro**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_search.png)

5. <span data-ttu-id="b1c78-135">Dans le volet de résultats, sélectionnez **UltiPro**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="b1c78-135">In the results panel, select **UltiPro**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b1c78-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b1c78-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b1c78-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec UltiPro avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="b1c78-138">In this section, you configure and test Azure AD single sign-on with UltiPro based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b1c78-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur UltiPro équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b1c78-139">For single sign-on to work, Azure AD needs to know what the counterpart user in UltiPro is to a user in Azure AD.</span></span> <span data-ttu-id="b1c78-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur UltiPro associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="b1c78-140">In other words, a link relationship between an Azure AD user and the related user in UltiPro needs to be established.</span></span>

<span data-ttu-id="b1c78-141">Dans UltiPro, assignez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **Username** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="b1c78-141">In UltiPro, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b1c78-142">Pour configurer et tester l’authentification unique Azure AD avec UltiPro, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="b1c78-142">To configure and test Azure AD single sign-on with UltiPro, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b1c78-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="b1c78-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b1c78-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b1c78-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b1c78-145">**[Création d’un utilisateur de test UltiPro](#creating-a-ultipro-test-user)** pour avoir un équivalent de Britta Simon dans UltiPro, lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="b1c78-145">**[Creating a UltiPro test user](#creating-a-ultipro-test-user)** - to have a counterpart of Britta Simon in UltiPro that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b1c78-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b1c78-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b1c78-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="b1c78-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b1c78-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b1c78-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b1c78-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application UltiPro.</span><span class="sxs-lookup"><span data-stu-id="b1c78-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your UltiPro application.</span></span>

<span data-ttu-id="b1c78-150">**Pour configurer l’authentification unique Azure AD avec UltiPro, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b1c78-150">**To configure Azure AD single sign-on with UltiPro, perform the following steps:**</span></span>

1. <span data-ttu-id="b1c78-151">Dans le portail Azure, dans la page d’intégration de l’application **UltiPro**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="b1c78-151">In the Azure portal, on the **UltiPro** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="b1c78-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="b1c78-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_samlbase.png)

3. <span data-ttu-id="b1c78-155">Dans la section **Domaine et URL UltiPro**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="b1c78-155">On the **UltiPro Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_url.png)

    <span data-ttu-id="b1c78-157">a.</span><span class="sxs-lookup"><span data-stu-id="b1c78-157">a.</span></span> <span data-ttu-id="b1c78-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant :</span><span class="sxs-lookup"><span data-stu-id="b1c78-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.ultipro.com/`|
    | `https://<companyname>.ultiproworkplace.com?cpi=AZUREADISSSUERURL`|
    | ` https://<companyname>.ultipro.ca`|
    
    <span data-ttu-id="b1c78-159">b.</span><span class="sxs-lookup"><span data-stu-id="b1c78-159">b.</span></span> <span data-ttu-id="b1c78-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant :</span><span class="sxs-lookup"><span data-stu-id="b1c78-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.ultipro.com/adfs/services/trust`|
    | `https://<companyname>.ultiproworkplace.com/adfs/services/trust`|
    | `https://<companyname>.ultipro.ca/adfs/services/trust`|
    
    <span data-ttu-id="b1c78-161">c.</span><span class="sxs-lookup"><span data-stu-id="b1c78-161">c.</span></span> <span data-ttu-id="b1c78-162">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant :</span><span class="sxs-lookup"><span data-stu-id="b1c78-162">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.ultipro.com/<instancename>`|
    | `https://<companyname>.ultiproworkplace.com/<instancename>`|
    | `https://<companyname>.ultipro.ca/<instancename>`|
    
    > [!NOTE] 
    > <span data-ttu-id="b1c78-163">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="b1c78-163">These values are not real.</span></span> <span data-ttu-id="b1c78-164">Mettez à jour ces valeurs avec l’identificateur, l’URL de réponse et l’URL de connexion réels.</span><span class="sxs-lookup"><span data-stu-id="b1c78-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="b1c78-165">Pour obtenir ces valeurs, contactez l’[équipe de support technique d’UltiPro](https://www.ultimatesoftware.com/ContactUs).</span><span class="sxs-lookup"><span data-stu-id="b1c78-165">Contact [UltiPro Client support team](https://www.ultimatesoftware.com/ContactUs) to get these values.</span></span> 

5. <span data-ttu-id="b1c78-166">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="b1c78-166">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_certificate.png) 

6. <span data-ttu-id="b1c78-168">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="b1c78-168">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ultipro-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="b1c78-170">Dans la section **Configuration de UltiPro**, cliquez sur **Configurer UltiPro** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="b1c78-170">On the **UltiPro Configuration** section, click **Configure UltiPro** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b1c78-171">Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="b1c78-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_configure.png) 

8. <span data-ttu-id="b1c78-173">Pour configurer l’authentification unique côté **UltiPro**, vous devez envoyer le **Certificat (Base64) téléchargé, l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à l’[équipe de support technique d’UltiPro](https://www.ultimatesoftware.com/ContactUs).</span><span class="sxs-lookup"><span data-stu-id="b1c78-173">To configure single sign-on on **UltiPro** side, you need to send the downloaded **Certificate(Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [UltiPro support team](https://www.ultimatesoftware.com/ContactUs).</span></span>

> [!TIP]
> <span data-ttu-id="b1c78-174">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="b1c78-174">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b1c78-175">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="b1c78-175">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b1c78-176">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b1c78-176">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b1c78-177">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="b1c78-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="b1c78-178">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="b1c78-178">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="b1c78-180">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b1c78-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b1c78-181">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b1c78-181">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ultipro-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b1c78-183">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="b1c78-183">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ultipro-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b1c78-185">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="b1c78-185">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ultipro-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b1c78-187">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="b1c78-187">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ultipro-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b1c78-189">a.</span><span class="sxs-lookup"><span data-stu-id="b1c78-189">a.</span></span> <span data-ttu-id="b1c78-190">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b1c78-190">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b1c78-191">b.</span><span class="sxs-lookup"><span data-stu-id="b1c78-191">b.</span></span> <span data-ttu-id="b1c78-192">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b1c78-192">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b1c78-193">c.</span><span class="sxs-lookup"><span data-stu-id="b1c78-193">c.</span></span> <span data-ttu-id="b1c78-194">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="b1c78-194">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b1c78-195">d.</span><span class="sxs-lookup"><span data-stu-id="b1c78-195">d.</span></span> <span data-ttu-id="b1c78-196">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="b1c78-196">Click **Create**.</span></span>
 
### <a name="creating-a-ultipro-test-user"></a><span data-ttu-id="b1c78-197">Création d’un utilisateur de test UltiPro</span><span class="sxs-lookup"><span data-stu-id="b1c78-197">Creating a UltiPro test user</span></span>

<span data-ttu-id="b1c78-198">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans UltiPro.</span><span class="sxs-lookup"><span data-stu-id="b1c78-198">In this section, you create a user called Britta Simon in UltiPro.</span></span> <span data-ttu-id="b1c78-199">Collaborez avec l’[équipe de support technique d’UltiPro](https://www.ultimatesoftware.com/ContactUs) pour ajouter les utilisateurs dans la plateforme UltiPro.</span><span class="sxs-lookup"><span data-stu-id="b1c78-199">Work with [UltiPro support team](https://www.ultimatesoftware.com/ContactUs) to add the users in the UltiPro platform.</span></span> <span data-ttu-id="b1c78-200">Les utilisateurs doivent être créés et activés avant que vous utilisiez l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="b1c78-200">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b1c78-201">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="b1c78-201">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b1c78-202">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à UltiPro.</span><span class="sxs-lookup"><span data-stu-id="b1c78-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to UltiPro.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="b1c78-204">**Pour affecter Britta Simon à UltiPro, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b1c78-204">**To assign Britta Simon to UltiPro, perform the following steps:**</span></span>

1. <span data-ttu-id="b1c78-205">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="b1c78-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="b1c78-207">Dans la liste des applications, sélectionnez **UltiPro**.</span><span class="sxs-lookup"><span data-stu-id="b1c78-207">In the applications list, select **UltiPro**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ultipro-tutorial/tutorial_ultipro_app.png) 

3. <span data-ttu-id="b1c78-209">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="b1c78-209">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="b1c78-211">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="b1c78-211">Click **Add** button.</span></span> <span data-ttu-id="b1c78-212">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="b1c78-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="b1c78-214">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="b1c78-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b1c78-215">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="b1c78-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b1c78-216">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="b1c78-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b1c78-217">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="b1c78-217">Testing single sign-on</span></span>

<span data-ttu-id="b1c78-218">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="b1c78-218">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="b1c78-219">Quand vous cliquez sur la vignette UltiPro dans le volet d’accès, vous êtes normalement connecté automatiquement à votre application UltiPro.</span><span class="sxs-lookup"><span data-stu-id="b1c78-219">When you click the UltiPro tile in the Access Panel, you should get automatically signed-on to your UltiPro application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b1c78-220">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="b1c78-220">Additional resources</span></span>

* [<span data-ttu-id="b1c78-221">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b1c78-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b1c78-222">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="b1c78-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ultipro-tutorial/tutorial_general_203.png

