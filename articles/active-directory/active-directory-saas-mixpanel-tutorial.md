---
title: "Didacticiel : Intégration d’Azure Active Directory à Mixpanel | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Mixpanel."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a2df26ef-d441-44ac-a9f3-b37bf9709bcb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 3dd11b3477de1329c1c8e45a6dbf212b1635fd95
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mixpanel"></a><span data-ttu-id="154c6-103">Didacticiel : Intégration d’Azure Active Directory à Mixpanel</span><span class="sxs-lookup"><span data-stu-id="154c6-103">Tutorial: Azure Active Directory integration with Mixpanel</span></span>

<span data-ttu-id="154c6-104">Dans ce didacticiel, vous allez apprendre à intégrer Mixpanel à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="154c6-104">In this tutorial, you learn how to integrate Mixpanel with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="154c6-105">L’intégration de Mixpanel dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="154c6-105">Integrating Mixpanel with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="154c6-106">Dans Azure AD, vous pouvez contrôler qui a accès à Mixpanel</span><span class="sxs-lookup"><span data-stu-id="154c6-106">You can control in Azure AD who has access to Mixpanel</span></span>
- <span data-ttu-id="154c6-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Mixpanel (via l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="154c6-107">You can enable your users to automatically get signed-on to Mixpanel (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="154c6-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="154c6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="154c6-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="154c6-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="154c6-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="154c6-110">Prerequisites</span></span>

<span data-ttu-id="154c6-111">Pour configurer l’intégration d’Azure AD avec Mixpanel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="154c6-111">To configure Azure AD integration with Mixpanel, you need the following items:</span></span>

- <span data-ttu-id="154c6-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="154c6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="154c6-113">Un abonnement Mixpanel pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="154c6-113">A Mixpanel single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="154c6-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="154c6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="154c6-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="154c6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="154c6-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="154c6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="154c6-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="154c6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="154c6-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="154c6-118">Scenario description</span></span>
<span data-ttu-id="154c6-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="154c6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="154c6-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="154c6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="154c6-121">Ajout de Mixpanel à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="154c6-121">Adding Mixpanel from the gallery</span></span>
2. <span data-ttu-id="154c6-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="154c6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mixpanel-from-the-gallery"></a><span data-ttu-id="154c6-123">Ajout de Mixpanel à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="154c6-123">Adding Mixpanel from the gallery</span></span>
<span data-ttu-id="154c6-124">Pour configurer l’intégration de Mixpanel à Azure AD, vous devez ajouter Mixpanel à votre liste d’applications SaaS gérées à partir de la galerie.</span><span class="sxs-lookup"><span data-stu-id="154c6-124">To configure the integration of Mixpanel into Azure AD, you need to add Mixpanel from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="154c6-125">**Pour ajouter Mixpanel à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="154c6-125">**To add Mixpanel from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="154c6-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="154c6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="154c6-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="154c6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="154c6-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="154c6-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="154c6-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="154c6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="154c6-133">Dans la zone de recherche, entrez **Mixpanel**.</span><span class="sxs-lookup"><span data-stu-id="154c6-133">In the search box, type **Mixpanel**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_search.png)

5. <span data-ttu-id="154c6-135">Dans le panneau des résultats, sélectionnez **Mixpanel**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="154c6-135">In the results panel, select **Mixpanel**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="154c6-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="154c6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="154c6-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Mixpanel avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="154c6-138">In this section, you configure and test Azure AD single sign-on with Mixpanel based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="154c6-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Mixpanel équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="154c6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Mixpanel is to a user in Azure AD.</span></span> <span data-ttu-id="154c6-140">En d’autres termes, il faut établir une relation entre l’utilisateur Azure AD et l’utilisateur Mixpanel associé.</span><span class="sxs-lookup"><span data-stu-id="154c6-140">In other words, a link relationship between an Azure AD user and the related user in Mixpanel needs to be established.</span></span>

<span data-ttu-id="154c6-141">Dans Mixpanel, assignez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="154c6-141">In Mixpanel, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="154c6-142">Pour configurer et tester l’authentification unique Azure AD avec Mixpanel, vous devez suivre les blocs élémentaires suivants :</span><span class="sxs-lookup"><span data-stu-id="154c6-142">To configure and test Azure AD single sign-on with Mixpanel, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="154c6-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="154c6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="154c6-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="154c6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="154c6-145">**[Création d’un utilisateur de test Mixpanel](#creating-a-mixpanel-test-user)** pour obtenir un équivalent de Britta Simon dans Mixpanel lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="154c6-145">**[Creating a Mixpanel test user](#creating-a-mixpanel-test-user)** - to have a counterpart of Britta Simon in Mixpanel that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="154c6-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="154c6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="154c6-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="154c6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="154c6-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="154c6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="154c6-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="154c6-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mixpanel application.</span></span>

<span data-ttu-id="154c6-150">**Pour configurer l’authentification unique Azure AD avec Mixpanel, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="154c6-150">**To configure Azure AD single sign-on with Mixpanel, perform the following steps:**</span></span>

1. <span data-ttu-id="154c6-151">Dans le portail Azure, sur la page d’intégration de l’application **Mixpanel**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="154c6-151">In the Azure portal, on the **Mixpanel** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="154c6-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="154c6-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_samlbase.png)

3. <span data-ttu-id="154c6-155">Dans la section **Domaine et URL Mixpanel**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="154c6-155">On the **Mixpanel Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_url.png)

     <span data-ttu-id="154c6-157">Dans la zone de texte **URL d’authentification**, tapez l’URL : `https://mixpanel.com/login/`</span><span class="sxs-lookup"><span data-stu-id="154c6-157">In the **Sign-on URL** textbox, type a URL as: `https://mixpanel.com/login/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="154c6-158">Inscrivez-vous à l’adresse [https://mixpanel.com/register/](https://mixpanel.com/register/) pour configurer vos informations d’identification et contactez [l’équipe du support technique Mixpanel](mailto:support@mixpanel.com) pour activer les paramètres d’authentification unique de votre abonné.</span><span class="sxs-lookup"><span data-stu-id="154c6-158">Please register at [https://mixpanel.com/register/](https://mixpanel.com/register/) to set up your login credentials and  contact the [Mixpanel support team](mailto:support@mixpanel.com) to enable SSO settings for your tenant.</span></span> <span data-ttu-id="154c6-159">Vous pouvez également obtenir la valeur de l’URL de connexion si nécessaire à partir de votre équipe de support Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="154c6-159">You can also get your Sign On URL value if necessary from your Mixpanel support team.</span></span> 
 
4. <span data-ttu-id="154c6-160">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="154c6-160">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_certificate.png) 

5. <span data-ttu-id="154c6-162">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="154c6-162">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-mixpanel-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="154c6-164">Dans la section **Configuration de Mixpanel**, cliquez sur **Configurer Mixpanel** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="154c6-164">On the **Mixpanel Configuration** section, click **Configure Mixpanel** to open **Configure sign-on** window.</span></span> <span data-ttu-id="154c6-165">Copiez l**’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="154c6-165">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_configure.png) 

7. <span data-ttu-id="154c6-167">Dans une autre fenêtre de navigateur, connectez-vous à votre application Mixpanel en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="154c6-167">In a different browser window, sign-on to your Mixpanel application as an administrator.</span></span>

8. <span data-ttu-id="154c6-168">Dans le coin gauche en bas de la page, cliquez sur l’icône représentant un petit **engrenage** .</span><span class="sxs-lookup"><span data-stu-id="154c6-168">On bottom of the page, click the little **gear** icon in the left corner.</span></span> 
   
    ![Authentification unique Mixpanel](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_06.png) 

9. <span data-ttu-id="154c6-170">Cliquez sur l’onglet **Sécurité d’accès**, puis cliquez sur **Modifier les paramètres**.</span><span class="sxs-lookup"><span data-stu-id="154c6-170">Click the **Access security** tab, and then click **Change settings**.</span></span>
   
    ![Paramètres Mixpanel](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_08.png) 

10. <span data-ttu-id="154c6-172">Sur la page **Modifier votre certificat**, cliquez sur **Choisir un fichier** pour importer votre certificat téléchargé, puis cliquez sur **SUIVANT**.</span><span class="sxs-lookup"><span data-stu-id="154c6-172">On the **Change your certificate** dialog page, click **Choose file** to upload your downloaded certificate, and then click **NEXT**.</span></span>
   
    ![Paramètres Mixpanel](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_09.png) 

11.  <span data-ttu-id="154c6-174">Dans la zone de texte URL d’authentification, sur la page de dialogue **Modifier l’URL d’authentification**, collez la valeur de l’**URL du service d’authentification unique SAML**, que vous avez copiée sur le portail Azure. Puis cliquez sur **SUIVANT**.</span><span class="sxs-lookup"><span data-stu-id="154c6-174">In the authentication URL textbox on the **Change your authentication  URL** dialog page, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal, and then click **NEXT**.</span></span>
   
   ![Paramètres Mixpanel](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_10.png) 

12. <span data-ttu-id="154c6-176">Cliquez sur **Done**.</span><span class="sxs-lookup"><span data-stu-id="154c6-176">Click **Done**.</span></span>

> [!TIP]
> <span data-ttu-id="154c6-177">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="154c6-177">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="154c6-178">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="154c6-178">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="154c6-179">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="154c6-179">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="154c6-180">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="154c6-180">Creating an Azure AD test user</span></span>
<span data-ttu-id="154c6-181">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="154c6-181">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="154c6-183">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="154c6-183">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="154c6-184">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="154c6-184">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="154c6-186">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="154c6-186">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="154c6-188">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="154c6-188">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="154c6-190">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="154c6-190">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mixpanel-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="154c6-192">a.</span><span class="sxs-lookup"><span data-stu-id="154c6-192">a.</span></span> <span data-ttu-id="154c6-193">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="154c6-193">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="154c6-194">b.</span><span class="sxs-lookup"><span data-stu-id="154c6-194">b.</span></span> <span data-ttu-id="154c6-195">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="154c6-195">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="154c6-196">c.</span><span class="sxs-lookup"><span data-stu-id="154c6-196">c.</span></span> <span data-ttu-id="154c6-197">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="154c6-197">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="154c6-198">d.</span><span class="sxs-lookup"><span data-stu-id="154c6-198">d.</span></span> <span data-ttu-id="154c6-199">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="154c6-199">Click **Create**.</span></span>
 
### <a name="creating-a-mixpanel-test-user"></a><span data-ttu-id="154c6-200">Création d’un utilisateur de test Mixpanel</span><span class="sxs-lookup"><span data-stu-id="154c6-200">Creating a Mixpanel test user</span></span>

<span data-ttu-id="154c6-201">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="154c6-201">The objective of this section is to create a user called Britta Simon in Mixpanel.</span></span> 

1. <span data-ttu-id="154c6-202">Connectez-vous à votre site d’entreprise Mixpanel en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="154c6-202">Sign on to your Mixpanel company site as an administrator.</span></span>

2. <span data-ttu-id="154c6-203">Dans le coin gauche en bas de la page, cliquez sur le bouton représentant un petit engrenage pour ouvrir la fenêtre **Paramètres** .</span><span class="sxs-lookup"><span data-stu-id="154c6-203">On the bottom of the page, click the little gear button on the left corner to open the **Settings** window.</span></span>

3. <span data-ttu-id="154c6-204">Cliquez sur l’onglet **Équipe** .</span><span class="sxs-lookup"><span data-stu-id="154c6-204">Click the **Team** tab.</span></span>

4. <span data-ttu-id="154c6-205">Dans la zone de texte **membre de l’équipe** , entrez l’adresse de messagerie de Britta dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="154c6-205">In the **team member** textbox, type Britta's email address in the Azure.</span></span>
   
    ![Paramètres Mixpanel](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_11.png) 

5. <span data-ttu-id="154c6-207">Cliquez sur **Inviter**.</span><span class="sxs-lookup"><span data-stu-id="154c6-207">Click **Invite**.</span></span> 

> [!Note]
> <span data-ttu-id="154c6-208">L’utilisateur recevra un e-mail pour configurer son profil.</span><span class="sxs-lookup"><span data-stu-id="154c6-208">The user will get an email to set up the profile.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="154c6-209">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="154c6-209">Assigning the Azure AD test user</span></span>

<span data-ttu-id="154c6-210">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="154c6-210">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mixpanel.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="154c6-212">**Pour affecter Britta Simon à Mixpanel, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="154c6-212">**To assign Britta Simon to Mixpanel, perform the following steps:**</span></span>

1. <span data-ttu-id="154c6-213">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="154c6-213">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="154c6-215">Dans la liste des applications, sélectionnez **Mixpanel**.</span><span class="sxs-lookup"><span data-stu-id="154c6-215">In the applications list, select **Mixpanel**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-mixpanel-tutorial/tutorial_mixpanel_app.png) 

3. <span data-ttu-id="154c6-217">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="154c6-217">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="154c6-219">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="154c6-219">Click **Add** button.</span></span> <span data-ttu-id="154c6-220">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="154c6-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="154c6-222">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="154c6-222">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="154c6-223">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="154c6-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="154c6-224">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="154c6-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="154c6-225">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="154c6-225">Testing single sign-on</span></span>

<span data-ttu-id="154c6-226">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="154c6-226">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="154c6-227">Lorsque vous cliquez sur la mosaïque Mixpanel dans le volet d’accès, vous êtes connecté automatiquement à votre application Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="154c6-227">When you click the Mixpanel tile in the Access Panel, you should get automatically signed-on to your Mixpanel application.</span></span>
<span data-ttu-id="154c6-228">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="154c6-228">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="154c6-229">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="154c6-229">Additional resources</span></span>

* [<span data-ttu-id="154c6-230">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="154c6-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="154c6-231">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="154c6-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mixpanel-tutorial/tutorial_general_203.png

