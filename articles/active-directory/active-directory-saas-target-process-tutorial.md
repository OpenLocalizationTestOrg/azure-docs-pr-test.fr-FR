---
title: "Didacticiel : Intégration d’Azure Active Directory à TargetProcess | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et TargetProcess."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 7cb91628-e758-480d-a233-7a3caaaff50d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: d15931a5d430252bbd9ae342e1f8fde1a539355b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-targetprocess"></a><span data-ttu-id="2f075-103">Didacticiel : Intégration d’Azure AD à TargetProcess</span><span class="sxs-lookup"><span data-stu-id="2f075-103">Tutorial: Azure Active Directory integration with TargetProcess</span></span>

<span data-ttu-id="2f075-104">Dans ce didacticiel, vous allez apprendre à intégrer TargetProcess à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2f075-104">In this tutorial, you learn how to integrate TargetProcess with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2f075-105">L’intégration de TargetProcess à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="2f075-105">Integrating TargetProcess with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2f075-106">Dans Azure AD, vous pouvez contrôler qui a accès à TargetProcess.</span><span class="sxs-lookup"><span data-stu-id="2f075-106">You can control in Azure AD who has access to TargetProcess</span></span>
- <span data-ttu-id="2f075-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à TargetProcess (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f075-107">You can enable your users to automatically get signed-on to TargetProcess (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2f075-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="2f075-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2f075-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2f075-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f075-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="2f075-110">Prerequisites</span></span>

<span data-ttu-id="2f075-111">Pour configurer l’intégration d’Azure AD avec TargetProcess, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="2f075-111">To configure Azure AD integration with TargetProcess, you need the following items:</span></span>

- <span data-ttu-id="2f075-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f075-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2f075-113">Un abonnement TargetProcess pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="2f075-113">A TargetProcess single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2f075-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="2f075-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2f075-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="2f075-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2f075-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="2f075-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2f075-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2f075-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2f075-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="2f075-118">Scenario description</span></span>
<span data-ttu-id="2f075-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="2f075-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2f075-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="2f075-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2f075-121">Ajouter TargetProcess à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="2f075-121">Add TargetProcess from the gallery</span></span>
2. <span data-ttu-id="2f075-122">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f075-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-targetprocess-from-the-gallery"></a><span data-ttu-id="2f075-123">Ajouter TargetProcess à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="2f075-123">Add TargetProcess from the gallery</span></span>
<span data-ttu-id="2f075-124">Pour configurer l’intégration de TargetProcess avec Azure AD, vous devez ajouter TargetProcess à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="2f075-124">To configure the integration of TargetProcess into Azure AD, you need to add TargetProcess from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2f075-125">**Pour ajouter TargetProcess à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2f075-125">**To add TargetProcess from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2f075-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2f075-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2f075-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="2f075-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2f075-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="2f075-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="2f075-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="2f075-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="2f075-133">Dans la zone de recherche, tapez **TargetProcess**, sélectionnez **TargetProcess** dans le volet de résultats, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="2f075-133">In the search box, type **TargetProcess**, select **TargetProcess**  from result panel then click **Add** button to add the application.</span></span>

    ![Ajouter TargetProcess à partir de la galerie](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="2f075-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f075-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="2f075-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD auprès de TargetProcess avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="2f075-136">In this section, you configure and test Azure AD single sign-on with TargetProcess based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2f075-137">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur TargetProcess équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f075-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TargetProcess is to a user in Azure AD.</span></span> <span data-ttu-id="2f075-138">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur TargetProcess associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="2f075-138">In other words, a link relationship between an Azure AD user and the related user in TargetProcess needs to be established.</span></span>

<span data-ttu-id="2f075-139">Dans TargetProcess, assignez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **Nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="2f075-139">In TargetProcess, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="2f075-140">Pour configurer et tester l’authentification unique Azure AD avec TargetProcess, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="2f075-140">To configure and test Azure AD single sign-on with TargetProcess, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2f075-141">**[Configurer l’authentification unique Azure AD](#configure-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="2f075-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2f075-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2f075-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2f075-143">**[Création d’un utilisateur de test TargetProcess](#create-a-targetprocess-test-user)** pour avoir un équivalent de Britta Simon dans TargetProcess lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="2f075-143">**[Create a TargetProcess test user](#create-a-targetprocess-test-user)** - to have a counterpart of Britta Simon in TargetProcess that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="2f075-144">**[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f075-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2f075-145">**[Tester l’authentification unique](#test-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="2f075-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="2f075-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f075-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="2f075-147">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application TargetProcess.</span><span class="sxs-lookup"><span data-stu-id="2f075-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TargetProcess application.</span></span>

<span data-ttu-id="2f075-148">**Pour configurer l’authentification unique Azure AD avec TargetProcess, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2f075-148">**To configure Azure AD single sign-on with TargetProcess, perform the following steps:**</span></span>

1. <span data-ttu-id="2f075-149">Dans le Portail Azure, dans la page d’intégration de l’application **TargetProcess**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="2f075-149">In the Azure portal, on the **TargetProcess** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="2f075-151">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="2f075-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Authentification basée sur SAML](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_samlbase.png)

3. <span data-ttu-id="2f075-153">Dans la section **Domaine et URL TargetProcess**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="2f075-153">On the **TargetProcess Domain and URLs** section, perform the following steps:</span></span>

    ![Section Domaine et URL TargetProcess](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_url.png)

    <span data-ttu-id="2f075-155">a.</span><span class="sxs-lookup"><span data-stu-id="2f075-155">a.</span></span> <span data-ttu-id="2f075-156">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<subdomain>.tpondemand.com/`</span><span class="sxs-lookup"><span data-stu-id="2f075-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.tpondemand.com/`</span></span>

    <span data-ttu-id="2f075-157">b.</span><span class="sxs-lookup"><span data-stu-id="2f075-157">b.</span></span> <span data-ttu-id="2f075-158">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<subdomain>.tpondemand.com/`</span><span class="sxs-lookup"><span data-stu-id="2f075-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.tpondemand.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2f075-159">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="2f075-159">These values are not real.</span></span> <span data-ttu-id="2f075-160">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="2f075-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="2f075-161">Pour obtenir ces valeurs, contactez l’[équipe de support client TargetProcess](mailto:support@targetprocess.com).</span><span class="sxs-lookup"><span data-stu-id="2f075-161">Contact [TargetProcess Client support team](mailto:support@targetprocess.com) to get these values.</span></span> 
 
4. <span data-ttu-id="2f075-162">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="2f075-162">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Section Certificat de signature SAML](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_certificate.png) 

5. <span data-ttu-id="2f075-164">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="2f075-164">Click **Save** button.</span></span>

    ![Bouton Enregistrer](./media/active-directory-saas-target-process-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2f075-166">Dans la section **Configuration de TargetProcess** , cliquez sur **Configurer TargetProcess** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="2f075-166">On the **TargetProcess Configuration** section, click **Configure TargetProcess** to open **Configure sign-on** window.</span></span> <span data-ttu-id="2f075-167">Copiez l**’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="2f075-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Section Configuration de TargetProcess](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_configure.png) 

7. <span data-ttu-id="2f075-169">Connectez-vous à votre application TargetProcess en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="2f075-169">Sign-on to your TargetProcess application as an administrator.</span></span>

8. <span data-ttu-id="2f075-170">Dans le menu situé en haut, cliquez sur **Setup**.</span><span class="sxs-lookup"><span data-stu-id="2f075-170">In the menu on the top, click **Setup**.</span></span>
   
    ![Paramétrage](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_05.png)

9. <span data-ttu-id="2f075-172">Cliquez sur **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="2f075-172">Click **Settings**.</span></span>
   
    ![Paramètres](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_06.png) 

10. <span data-ttu-id="2f075-174">Cliquez sur **Single Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="2f075-174">Click **Single Sign-on**.</span></span>
   
    ![Cliquer sur Authentification unique](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_07.png) 

11. <span data-ttu-id="2f075-176">Dans la boîte de dialogue Paramètres d’authentification unique, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="2f075-176">On the Single Sign-on settings dialog, perform the following steps:</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_08.png)
    
    <span data-ttu-id="2f075-178">a.</span><span class="sxs-lookup"><span data-stu-id="2f075-178">a.</span></span> <span data-ttu-id="2f075-179">Cliquez sur **Enable Single Sign-on**.</span><span class="sxs-lookup"><span data-stu-id="2f075-179">Click **Enable Single Sign-on**.</span></span>
    
    <span data-ttu-id="2f075-180">b.</span><span class="sxs-lookup"><span data-stu-id="2f075-180">b.</span></span> <span data-ttu-id="2f075-181">Dans la zone de texte **URL de connexion**, collez la valeur de l’**URL du service d’authentification unique SAML** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2f075-181">In **Sign-on URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="2f075-182">c.</span><span class="sxs-lookup"><span data-stu-id="2f075-182">c.</span></span> <span data-ttu-id="2f075-183">Ouvrez le certificat que vous avez téléchargé dans le Bloc-notes, copiez son contenu, puis collez-le dans la zone de texte **Certificat**.</span><span class="sxs-lookup"><span data-stu-id="2f075-183">Open your downloaded certificate in notepad, copy the content, and then paste it into the **Certificate** textbox.</span></span>
    
    <span data-ttu-id="2f075-184">d.</span><span class="sxs-lookup"><span data-stu-id="2f075-184">d.</span></span> <span data-ttu-id="2f075-185">Cliquez sur **Activer la configuration JIT**.</span><span class="sxs-lookup"><span data-stu-id="2f075-185">click **Enable JIT Provisioning**.</span></span>

    <span data-ttu-id="2f075-186">e.</span><span class="sxs-lookup"><span data-stu-id="2f075-186">e.</span></span> <span data-ttu-id="2f075-187">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="2f075-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="2f075-188">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="2f075-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2f075-189">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="2f075-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2f075-190">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2f075-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="2f075-191">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f075-191">Create an Azure AD test user</span></span>
<span data-ttu-id="2f075-192">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2f075-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="2f075-194">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2f075-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2f075-195">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2f075-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-target-process-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2f075-197">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="2f075-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Pour afficher la liste des utilisateurs](./media/active-directory-saas-target-process-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2f075-199">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="2f075-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Bouton Ajouter](./media/active-directory-saas-target-process-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2f075-201">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="2f075-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Section Utilisateur](./media/active-directory-saas-target-process-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2f075-203">a.</span><span class="sxs-lookup"><span data-stu-id="2f075-203">a.</span></span> <span data-ttu-id="2f075-204">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2f075-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2f075-205">b.</span><span class="sxs-lookup"><span data-stu-id="2f075-205">b.</span></span> <span data-ttu-id="2f075-206">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2f075-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2f075-207">c.</span><span class="sxs-lookup"><span data-stu-id="2f075-207">c.</span></span> <span data-ttu-id="2f075-208">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="2f075-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2f075-209">d.</span><span class="sxs-lookup"><span data-stu-id="2f075-209">d.</span></span> <span data-ttu-id="2f075-210">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="2f075-210">Click **Create**.</span></span>
 
### <a name="create-a-targetprocess-test-user"></a><span data-ttu-id="2f075-211">Créer un utilisateur de test TargetProcess</span><span class="sxs-lookup"><span data-stu-id="2f075-211">Create a TargetProcess test user</span></span>

<span data-ttu-id="2f075-212">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans TargetProcess.</span><span class="sxs-lookup"><span data-stu-id="2f075-212">The objective of this section is to create a user called Britta Simon in TargetProcess.</span></span>

<span data-ttu-id="2f075-213">TargetProcess prend en charge l’approvisionnement juste-à-temps.</span><span class="sxs-lookup"><span data-stu-id="2f075-213">TargetProcess supports just-in-time provisioning.</span></span> <span data-ttu-id="2f075-214">Vous l’avez déjà activé dans [Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="2f075-214">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="2f075-215">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="2f075-215">There is no action item for you in this section.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="2f075-216">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f075-216">Assign the Azure AD test user</span></span>

<span data-ttu-id="2f075-217">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à TargetProcess.</span><span class="sxs-lookup"><span data-stu-id="2f075-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TargetProcess.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="2f075-219">**Pour affecter Britta Simon à TargetProcess, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2f075-219">**To assign Britta Simon to TargetProcess, perform the following steps:**</span></span>

1. <span data-ttu-id="2f075-220">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="2f075-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="2f075-222">Dans la liste des applications, sélectionnez **TargetProcess**.</span><span class="sxs-lookup"><span data-stu-id="2f075-222">In the applications list, select **TargetProcess**.</span></span>

    ![TargetProcess dans la liste des applications](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_app.png) 

3. <span data-ttu-id="2f075-224">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="2f075-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="2f075-226">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="2f075-226">Click **Add** button.</span></span> <span data-ttu-id="2f075-227">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="2f075-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="2f075-229">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="2f075-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2f075-230">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="2f075-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2f075-231">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="2f075-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="2f075-232">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="2f075-232">Test single sign-on</span></span>

<span data-ttu-id="2f075-233">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="2f075-233">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2f075-234">Lorsque vous cliquez sur la vignette TargetProcess dans le volet d’accès, vous devez être connecté automatiquement à votre application TargetProcess.</span><span class="sxs-lookup"><span data-stu-id="2f075-234">When you click the TargetProcess tile in the Access Panel, you should get automatically signed-on to your TargetProcess application.</span></span> <span data-ttu-id="2f075-235">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2f075-235">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2f075-236">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="2f075-236">Additional resources</span></span>

* [<span data-ttu-id="2f075-237">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2f075-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2f075-238">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="2f075-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_203.png

