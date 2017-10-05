---
title: "Didacticiel : Intégration d’Azure Active Directory à AnswerHub | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et AnswerHub."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 818b91d7-01df-4b36-9706-f167c710a73c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 3a1c9cc5d7a2ebe28e9fb7e0e6ed8e3d393873ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-answerhub"></a><span data-ttu-id="700a4-103">Didacticiel : Intégration d’Azure Active Directory à AnswerHub</span><span class="sxs-lookup"><span data-stu-id="700a4-103">Tutorial: Azure Active Directory integration with AnswerHub</span></span>

<span data-ttu-id="700a4-104">Dans ce didacticiel, vous allez apprendre à intégrer AnswerHub à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="700a4-104">In this tutorial, you learn how to integrate AnswerHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="700a4-105">L’intégration d’AnswerHub dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="700a4-105">Integrating AnswerHub with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="700a4-106">Dans Azure AD, vous pouvez contrôler qui a accès à AnswerHub</span><span class="sxs-lookup"><span data-stu-id="700a4-106">You can control in Azure AD who has access to AnswerHub</span></span>
- <span data-ttu-id="700a4-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à AnswerHub (par le biais de l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="700a4-107">You can enable your users to automatically get signed-on to AnswerHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="700a4-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="700a4-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="700a4-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="700a4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="700a4-110">Prérequis</span><span class="sxs-lookup"><span data-stu-id="700a4-110">Prerequisites</span></span>

<span data-ttu-id="700a4-111">Pour configurer l’intégration d’Azure AD à AnswerHub, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="700a4-111">To configure Azure AD integration with AnswerHub, you need the following items:</span></span>

- <span data-ttu-id="700a4-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="700a4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="700a4-113">Un abonnement AnswerHub pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="700a4-113">An AnswerHub single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="700a4-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="700a4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="700a4-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="700a4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="700a4-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="700a4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="700a4-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="700a4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="700a4-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="700a4-118">Scenario description</span></span>
<span data-ttu-id="700a4-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="700a4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="700a4-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="700a4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="700a4-121">Ajout d’AnswerHub à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="700a4-121">Adding AnswerHub from the gallery</span></span>
2. <span data-ttu-id="700a4-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="700a4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-answerhub-from-the-gallery"></a><span data-ttu-id="700a4-123">Ajout d’AnswerHub à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="700a4-123">Adding AnswerHub from the gallery</span></span>
<span data-ttu-id="700a4-124">Pour configurer l’intégration d’AnswerHub à Azure AD, vous devez ajouter AnswerHub depuis la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="700a4-124">To configure the integration of AnswerHub into Azure AD, you need to add AnswerHub from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="700a4-125">**Pour ajouter AnswerHub à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="700a4-125">**To add AnswerHub from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="700a4-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="700a4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="700a4-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="700a4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="700a4-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="700a4-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="700a4-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="700a4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="700a4-133">Dans la zone de recherche, tapez **AnswerHub**.</span><span class="sxs-lookup"><span data-stu-id="700a4-133">In the search box, type **AnswerHub**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_search.png)

5. <span data-ttu-id="700a4-135">Dans le volet de résultats, sélectionnez **AnswerHub**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="700a4-135">In the results panel, select **AnswerHub**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="700a4-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="700a4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="700a4-138">Dans cette section, vous configurez et testez l’authentification unique Azure AD avec AnswerHub au moyen d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="700a4-138">In this section, you configure and test Azure AD single sign-on with AnswerHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="700a4-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur AnswerHub équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="700a4-139">For single sign-on to work, Azure AD needs to know what the counterpart user in AnswerHub is to a user in Azure AD.</span></span> <span data-ttu-id="700a4-140">En d’autres termes, une relation entre un utilisateur Azure AD et l’utilisateur AnswerHub associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="700a4-140">In other words, a link relationship between an Azure AD user and the related user in AnswerHub needs to be established.</span></span>

<span data-ttu-id="700a4-141">Dans AnswerHub, affectez la valeur du **nom d’utilisateur** indiquée dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="700a4-141">In AnswerHub, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="700a4-142">Pour configurer et tester l’authentification unique Azure AD avec AnswerHub, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="700a4-142">To configure and test Azure AD single sign-on with AnswerHub, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="700a4-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="700a4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="700a4-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="700a4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="700a4-145">**[Création d’un utilisateur de test AnswerHub](#creating-an-answerhub-test-user)** pour avoir dans AnswerHub un équivalent de Britta Simon lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="700a4-145">**[Creating an AnswerHub test user](#creating-an-answerhub-test-user)** - to have a counterpart of Britta Simon in AnswerHub that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="700a4-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="700a4-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="700a4-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="700a4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="700a4-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="700a4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="700a4-149">Dans cette section, vous activez l’authentification unique Azure AD dans le portail Azure et configurez l’authentification unique dans votre application AnswerHub.</span><span class="sxs-lookup"><span data-stu-id="700a4-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your AnswerHub application.</span></span>

<span data-ttu-id="700a4-150">**Pour configurer l’authentification unique Azure AD avec AnswerHub, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="700a4-150">**To configure Azure AD single sign-on with AnswerHub, perform the following steps:**</span></span>

1. <span data-ttu-id="700a4-151">Dans le portail Azure, sur la page d’intégration de l’application **AnswerHub**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="700a4-151">In the Azure portal, on the **AnswerHub** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="700a4-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="700a4-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_samlbase.png)

3. <span data-ttu-id="700a4-155">Dans la section **Domaine et URL AnswerHub**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="700a4-155">On the **AnswerHub Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_url.png)

    <span data-ttu-id="700a4-157">a.</span><span class="sxs-lookup"><span data-stu-id="700a4-157">a.</span></span> <span data-ttu-id="700a4-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<company>.answerhub.com`</span><span class="sxs-lookup"><span data-stu-id="700a4-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company>.answerhub.com`</span></span>

    <span data-ttu-id="700a4-159">b.</span><span class="sxs-lookup"><span data-stu-id="700a4-159">b.</span></span> <span data-ttu-id="700a4-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<company>.answerhub.com`</span><span class="sxs-lookup"><span data-stu-id="700a4-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company>.answerhub.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="700a4-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="700a4-161">These values are not real.</span></span> <span data-ttu-id="700a4-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="700a4-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="700a4-163">Pour obtenir ces valeurs, contactez l’[équipe du support technique d’AnswerHub](mailto:success@answerhub.com).</span><span class="sxs-lookup"><span data-stu-id="700a4-163">Contact [AnswerHub Client support team](mailto:success@answerhub.com) to get these values.</span></span> 
 
4. <span data-ttu-id="700a4-164">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="700a4-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_certificate.png) 

5. <span data-ttu-id="700a4-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="700a4-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-answerhub-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="700a4-168">Dans la section **Configuration AnswerHub**, cliquez sur **Configurer AnswerHub** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="700a4-168">On the **AnswerHub Configuration** section, click **Configure AnswerHub** to open **Configure sign-on** window.</span></span> <span data-ttu-id="700a4-169">Copiez **l’URL de déconnexion et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="700a4-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_configure.png) 

7. <span data-ttu-id="700a4-171">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise AnswerHub en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="700a4-171">In a different web browser window, log into your AnswerHub company site as an administrator.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="700a4-172">Si vous avez besoin d’aide pour la configuration d’AnswerHub, contactez [l’équipe de support technique de AnswerHub](mailto:success@answerhub.com.).</span><span class="sxs-lookup"><span data-stu-id="700a4-172">If you need help configuring AnswerHub, contact [AnswerHub's support team](mailto:success@answerhub.com.).</span></span>
   
8. <span data-ttu-id="700a4-173">Accédez à **Administration**.</span><span class="sxs-lookup"><span data-stu-id="700a4-173">Go to **Administration**.</span></span>

9. <span data-ttu-id="700a4-174">Cliquez sur l’onglet **Users &amp; Groups** .</span><span class="sxs-lookup"><span data-stu-id="700a4-174">Click the **User and Group** tab.</span></span>

10. <span data-ttu-id="700a4-175">Dans le volet de navigation situé sur le côté gauche, dans la section **Social Settings**, cliquez sur **SAML Setup**.</span><span class="sxs-lookup"><span data-stu-id="700a4-175">In the navigation pane on the left side, in the **Social Settings** section, click **SAML Setup**.</span></span>

11. <span data-ttu-id="700a4-176">Cliquez sur l’onglet **IDP Config** .</span><span class="sxs-lookup"><span data-stu-id="700a4-176">Click **IDP Config** tab.</span></span>

12. <span data-ttu-id="700a4-177">Sous l’onglet **IDP Config** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="700a4-177">On the **IDP Config** tab, perform the following steps:</span></span>

     <span data-ttu-id="700a4-178">![Configuration de SAML](./media/active-directory-saas-answerhub-tutorial/ic785172.png "Configuration de SAML")</span><span class="sxs-lookup"><span data-stu-id="700a4-178">![SAML Setup](./media/active-directory-saas-answerhub-tutorial/ic785172.png "SAML Setup")</span></span>  
  
     <span data-ttu-id="700a4-179">a.</span><span class="sxs-lookup"><span data-stu-id="700a4-179">a.</span></span> <span data-ttu-id="700a4-180">Dans la zone de texte **IDP Login URL** (URL de connexion du fournisseur d’identité), collez l’**URL du service d’authentification unique SAML** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="700a4-180">In **IDP Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
     <span data-ttu-id="700a4-181">b.</span><span class="sxs-lookup"><span data-stu-id="700a4-181">b.</span></span> <span data-ttu-id="700a4-182">Dans la zone de texte **IDP Logout URL** (URL de déconnexion du fournisseur d’identité), collez la valeur de l’**URL de déconnexion** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="700a4-182">In **IDP Logout URL** textbox, paste **Sign-Out URL** value which you have copied from Azure portal.</span></span>
     
     <span data-ttu-id="700a4-183">c.</span><span class="sxs-lookup"><span data-stu-id="700a4-183">c.</span></span> <span data-ttu-id="700a4-184">Dans la zone de texte **IDP Name Identifier Format** (Format de l’identificateur du nom IDP), entrez la valeur de l’identificateur d’utilisateur telle que sélectionnée dans le portail Azure à la section **Attributs utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="700a4-184">In **IDP Name Identifier Format** textbox, enter the user Identifier value same as selected in Azure portal in **User Attributes** section.</span></span>
  
     <span data-ttu-id="700a4-185">d.</span><span class="sxs-lookup"><span data-stu-id="700a4-185">d.</span></span> <span data-ttu-id="700a4-186">Cliquez sur **Keys and Certificates**.</span><span class="sxs-lookup"><span data-stu-id="700a4-186">Click **Keys and Certificates**.</span></span>

13. <span data-ttu-id="700a4-187">Sous l’onglet Keys and Certificates, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="700a4-187">On the Keys and Certificates tab, perform the following steps:</span></span>
    
     <span data-ttu-id="700a4-188">![Clés et certificats](./media/active-directory-saas-answerhub-tutorial/ic785173.png "Clés et certificats")</span><span class="sxs-lookup"><span data-stu-id="700a4-188">![Keys and Certificates](./media/active-directory-saas-answerhub-tutorial/ic785173.png "Keys and Certificates")</span></span>  
 
     <span data-ttu-id="700a4-189">a.</span><span class="sxs-lookup"><span data-stu-id="700a4-189">a.</span></span> <span data-ttu-id="700a4-190">Dans le Bloc-notes, ouvrez le certificat codé en base 64 que vous avez téléchargé depuis le portail Azure, copiez son contenu dans le Presse-papiers, puis collez-le dans la zone de texte **IDP Public Key (x509 Format)** (Clé publique IDP au format x509).</span><span class="sxs-lookup"><span data-stu-id="700a4-190">Open your base-64 encoded certificate which you have downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **IDP Public Key (x509 Format)** textbox.</span></span>
  
     <span data-ttu-id="700a4-191">b.</span><span class="sxs-lookup"><span data-stu-id="700a4-191">b.</span></span> <span data-ttu-id="700a4-192">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="700a4-192">Click **Save**.</span></span>

14. <span data-ttu-id="700a4-193">Sous l’onglet **IDP Config**, cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="700a4-193">On the **IDP Config** tab, click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="700a4-194">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="700a4-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="700a4-195">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="700a4-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="700a4-196">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="700a4-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="700a4-197">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="700a4-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="700a4-198">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="700a4-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="700a4-200">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="700a4-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="700a4-201">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="700a4-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-answerhub-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="700a4-203">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="700a4-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-answerhub-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="700a4-205">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="700a4-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-answerhub-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="700a4-207">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="700a4-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-answerhub-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="700a4-209">a.</span><span class="sxs-lookup"><span data-stu-id="700a4-209">a.</span></span> <span data-ttu-id="700a4-210">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="700a4-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="700a4-211">b.</span><span class="sxs-lookup"><span data-stu-id="700a4-211">b.</span></span> <span data-ttu-id="700a4-212">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="700a4-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="700a4-213">c.</span><span class="sxs-lookup"><span data-stu-id="700a4-213">c.</span></span> <span data-ttu-id="700a4-214">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="700a4-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="700a4-215">d.</span><span class="sxs-lookup"><span data-stu-id="700a4-215">d.</span></span> <span data-ttu-id="700a4-216">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="700a4-216">Click **Create**.</span></span>
 
### <a name="creating-an-answerhub-test-user"></a><span data-ttu-id="700a4-217">Création d’un utilisateur de test AnswerHub</span><span class="sxs-lookup"><span data-stu-id="700a4-217">Creating an AnswerHub test user</span></span>

<span data-ttu-id="700a4-218">Pour permettre aux utilisateurs Azure AD de se connecter à AnswerHub, vous devez les approvisionner dans AnswerHub.</span><span class="sxs-lookup"><span data-stu-id="700a4-218">To enable Azure AD users to log in to AnswerHub, they must be provisioned into AnswerHub.</span></span>  
<span data-ttu-id="700a4-219">Dans le cas d’AnswerHub, cet approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="700a4-219">In the case of AnswerHub, provisioning is a manual task.</span></span>

<span data-ttu-id="700a4-220">**Pour approvisionner un compte d’utilisateur, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="700a4-220">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="700a4-221">Connectez-vous à votre site d’entreprise **AnswerHub** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="700a4-221">Log in to your **AnswerHub** company site as administrator.</span></span>

2. <span data-ttu-id="700a4-222">Accédez à **Administration**.</span><span class="sxs-lookup"><span data-stu-id="700a4-222">Go to **Administration**.</span></span>

3. <span data-ttu-id="700a4-223">Cliquez sur l’onglet **Users & Groups**.</span><span class="sxs-lookup"><span data-stu-id="700a4-223">Click the **Users & Groups** tab.</span></span>

4. <span data-ttu-id="700a4-224">Dans le volet de navigation situé sur le côté gauche, dans la section **Manage Users**, cliquez sur **Create or import users**.</span><span class="sxs-lookup"><span data-stu-id="700a4-224">In the navigation pane on the left side, in the **Manage Users** section, click **Create or import users**.</span></span>
   
   <span data-ttu-id="700a4-225">![Utilisateurs et groupes](./media/active-directory-saas-answerhub-tutorial/ic785175.png "Utilisateurs et groupes")</span><span class="sxs-lookup"><span data-stu-id="700a4-225">![Users & Groups](./media/active-directory-saas-answerhub-tutorial/ic785175.png "Users & Groups")</span></span>

5. <span data-ttu-id="700a4-226">Tapez l’adresse e-mail, le nom d’utilisateur et le mot de passe du compte d’utilisateur Azure Active Directory valide que vous souhaitez approvisionner dans les zones de texte correspondantes, à savoir, **Email address**, **Username** et **Password**, puis cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="700a4-226">Type the **Email address**, **Username** and **Password** of a valid Azure Active Directory account you want to provision into the related textboxes, and then click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="700a4-227">Vous pouvez utiliser n'importe quel autre outil ou API de création de compte d’utilisateur AnswerHub fourni par ce service pour approvisionner des comptes utilisateurs AAD.</span><span class="sxs-lookup"><span data-stu-id="700a4-227">You can use any other AnswerHub user account creation tools or APIs provided by AnswerHub to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="700a4-228">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="700a4-228">Assigning the Azure AD test user</span></span>

<span data-ttu-id="700a4-229">Dans cette section, vous autorisez Britta Simon à utiliser l’authentification unique Azure en accordant l’accès à AnswerHub.</span><span class="sxs-lookup"><span data-stu-id="700a4-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to AnswerHub.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="700a4-231">**Pour affecter Britta Simon à AnswerHub, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="700a4-231">**To assign Britta Simon to AnswerHub, perform the following steps:**</span></span>

1. <span data-ttu-id="700a4-232">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="700a4-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="700a4-234">Dans la liste des applications, sélectionnez **AnswerHub**.</span><span class="sxs-lookup"><span data-stu-id="700a4-234">In the applications list, select **AnswerHub**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-answerhub-tutorial/tutorial_answerhub_app.png) 

3. <span data-ttu-id="700a4-236">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="700a4-236">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="700a4-238">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="700a4-238">Click **Add** button.</span></span> <span data-ttu-id="700a4-239">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="700a4-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="700a4-241">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="700a4-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="700a4-242">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="700a4-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="700a4-243">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="700a4-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="700a4-244">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="700a4-244">Testing single sign-on</span></span>

<span data-ttu-id="700a4-245">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="700a4-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="700a4-246">Lorsque vous cliquez sur la vignette AnswerHub dans le volet d’accès, vous devez automatiquement être connecté à votre application AnswerHub.</span><span class="sxs-lookup"><span data-stu-id="700a4-246">When you click the AnswerHub tile in the Access Panel, you should get automatically signed-on to your AnswerHub application.</span></span>
<span data-ttu-id="700a4-247">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="700a4-247">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="700a4-248">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="700a4-248">Additional resources</span></span>

* [<span data-ttu-id="700a4-249">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="700a4-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="700a4-250">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="700a4-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-answerhub-tutorial/tutorial_general_203.png

