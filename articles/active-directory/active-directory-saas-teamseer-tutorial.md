---
title: "Didacticiel : Intégration d’Azure Active Directory à TeamSeer | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et TeamSeer."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6ec4806f-fe0f-4ed7-8cfa-32d1c840433f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 2a5e8f6d1443681c43db95da5cef0b7f2ef92291
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamseer"></a><span data-ttu-id="98521-103">Didacticiel : Intégration d’Azure AD à TeamSeer</span><span class="sxs-lookup"><span data-stu-id="98521-103">Tutorial: Azure Active Directory integration with TeamSeer</span></span>

<span data-ttu-id="98521-104">Dans ce didacticiel, vous allez apprendre à intégrer TeamSeer à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="98521-104">In this tutorial, you learn how to integrate TeamSeer with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="98521-105">L’intégration de TeamSeer à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="98521-105">Integrating TeamSeer with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="98521-106">Dans Azure AD, vous pouvez contrôler qui a accès à TeamSeer.</span><span class="sxs-lookup"><span data-stu-id="98521-106">You can control in Azure AD who has access to TeamSeer</span></span>
- <span data-ttu-id="98521-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à TeamSeer (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="98521-107">You can enable your users to automatically get signed-on to TeamSeer (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="98521-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="98521-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="98521-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="98521-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="98521-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="98521-110">Prerequisites</span></span>

<span data-ttu-id="98521-111">Pour configurer l’intégration d’Azure AD à TeamSeer, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="98521-111">To configure Azure AD integration with TeamSeer, you need the following items:</span></span>

- <span data-ttu-id="98521-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="98521-112">An Azure AD subscription</span></span>
- <span data-ttu-id="98521-113">Un abonnement TeamSeer pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="98521-113">A TeamSeer single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="98521-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="98521-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="98521-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="98521-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="98521-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="98521-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="98521-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="98521-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="98521-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="98521-118">Scenario description</span></span>
<span data-ttu-id="98521-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="98521-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="98521-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="98521-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="98521-121">Ajout de TeamSeer à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="98521-121">Adding TeamSeer from the gallery</span></span>
2. <span data-ttu-id="98521-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="98521-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-teamseer-from-the-gallery"></a><span data-ttu-id="98521-123">Ajout de TeamSeer à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="98521-123">Adding TeamSeer from the gallery</span></span>
<span data-ttu-id="98521-124">Pour configurer l’intégration de TeamSeer à Azure AD, vous devez ajouter TeamSeer à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="98521-124">To configure the integration of TeamSeer in to Azure AD, you need to add TeamSeer from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="98521-125">**Pour ajouter TeamSeer à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="98521-125">**To add TeamSeer from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="98521-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="98521-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="98521-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="98521-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="98521-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="98521-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="98521-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="98521-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="98521-133">Dans la zone de recherche, tapez **TeamSeer**.</span><span class="sxs-lookup"><span data-stu-id="98521-133">In the search box, type **TeamSeer**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_search.png)

5. <span data-ttu-id="98521-135">Dans le panneau de résultats, sélectionnez **TeamSeer**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="98521-135">In the results panel, select **TeamSeer**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="98521-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="98521-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="98521-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec TeamSeer à l’aide d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="98521-138">In this section, you configure and test Azure AD single sign-on with TeamSeer based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="98521-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur TeamSeer équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="98521-139">For single sign-on to work, Azure AD needs to know what the counterpart user in TeamSeer is to a user in Azure AD.</span></span> <span data-ttu-id="98521-140">En d’autres termes, une relation entre un utilisateur Azure AD et l’utilisateur TeamSeer associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="98521-140">In other words, a link relationship between an Azure AD user and the related user in TeamSeer needs to be established.</span></span>

<span data-ttu-id="98521-141">Dans TeamSeer, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="98521-141">In TeamSeer, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="98521-142">Pour configurer et tester l’authentification unique Azure AD avec TeamSeer, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="98521-142">To configure and test Azure AD single sign-on with TeamSeer, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="98521-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="98521-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="98521-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="98521-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="98521-145">**[Création d’un utilisateur de test TeamSeer](#creating-a-teamseer-test-user)** pour avoir un équivalent de Britta Simon dans TeamSeer lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="98521-145">**[Creating a TeamSeer test user](#creating-a-teamseer-test-user)** - to have a counterpart of Britta Simon in TeamSeer that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="98521-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="98521-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="98521-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="98521-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="98521-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="98521-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="98521-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application TeamSeer.</span><span class="sxs-lookup"><span data-stu-id="98521-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TeamSeer application.</span></span>

<span data-ttu-id="98521-150">**Pour configurer l’authentification unique Azure AD avec TeamSeer, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="98521-150">**To configure Azure AD single sign-on with TeamSeer, perform the following steps:**</span></span>

1. <span data-ttu-id="98521-151">Dans le portail Azure, sur la page d’intégration de l’application **TeamSeer**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="98521-151">In the Azure portal, on the **TeamSeer** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="98521-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="98521-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_samlbase.png)

3. <span data-ttu-id="98521-155">Dans la section **TeamSeer Domain and URLs** (Domaine et URL TeamSeer), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="98521-155">On the **TeamSeer Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_url.png)

     <span data-ttu-id="98521-157">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://www.teamseer.com/<companyid>`</span><span class="sxs-lookup"><span data-stu-id="98521-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.teamseer.com/<companyid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="98521-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="98521-158">The value is not real.</span></span> <span data-ttu-id="98521-159">Mettez à jour la valeur avec l’URL de connexion réelle.</span><span class="sxs-lookup"><span data-stu-id="98521-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="98521-160">Pour obtenir cette valeur, contactez [l’équipe de support technique TeamSeer](http://pages.theaccessgroup.com/solutions_business-suite_absence-management_contact.html).</span><span class="sxs-lookup"><span data-stu-id="98521-160">Contact [TeamSeer Client support team](http://pages.theaccessgroup.com/solutions_business-suite_absence-management_contact.html) to get the value.</span></span> 
 
4. <span data-ttu-id="98521-161">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="98521-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_certificate.png) 

5. <span data-ttu-id="98521-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="98521-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-teamseer-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="98521-165">Dans la section **TeamSeer Configuration** (Configuration de TeamSeer), cliquez sur **Configure TeamSeer** (Configurer TeamSeer) pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="98521-165">On the **TeamSeer Configuration** section, click **Configure TeamSeer** to open **Configure sign-on** window.</span></span> <span data-ttu-id="98521-166">Copiez l**’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="98521-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_configure.png)

7. <span data-ttu-id="98521-168">Dans une autre fenêtre de navigateur web, connectez-vous au site de votre entreprise TeamSeer en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="98521-168">In a different web browser window, log in to your TeamSeer company site as an administrator.</span></span>

8. <span data-ttu-id="98521-169">Accédez à **HR Admin**.</span><span class="sxs-lookup"><span data-stu-id="98521-169">Go to **HR Admin**.</span></span>
   
    <span data-ttu-id="98521-170">![Administrateur RH](./media/active-directory-saas-teamseer-tutorial/ic789634.png "Administrateur RH")</span><span class="sxs-lookup"><span data-stu-id="98521-170">![HR Admin](./media/active-directory-saas-teamseer-tutorial/ic789634.png "HR Admin")</span></span>

9. <span data-ttu-id="98521-171">Cliquez sur **Setup**.</span><span class="sxs-lookup"><span data-stu-id="98521-171">Click **Setup**.</span></span>
   
    <span data-ttu-id="98521-172">![Configuration](./media/active-directory-saas-teamseer-tutorial/ic789635.png "Configuration")</span><span class="sxs-lookup"><span data-stu-id="98521-172">![Setup](./media/active-directory-saas-teamseer-tutorial/ic789635.png "Setup")</span></span>

10. <span data-ttu-id="98521-173">Cliquez sur **Set up SAML provider details**.</span><span class="sxs-lookup"><span data-stu-id="98521-173">Click **Set up SAML provider details**.</span></span>
   
    <span data-ttu-id="98521-174">![Paramètres SAML](./media/active-directory-saas-teamseer-tutorial/ic789636.png "Paramètres SAML")</span><span class="sxs-lookup"><span data-stu-id="98521-174">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789636.png "SAML Settings")</span></span>

11. <span data-ttu-id="98521-175">Dans la section des détails sur le fournisseur SAML, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="98521-175">In the SAML provider details section, perform the following steps:</span></span>
   
    <span data-ttu-id="98521-176">![Paramètres SAML](./media/active-directory-saas-teamseer-tutorial/ic789637.png "Paramètres SAML")</span><span class="sxs-lookup"><span data-stu-id="98521-176">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789637.png "SAML Settings")</span></span>   

    <span data-ttu-id="98521-177">a.</span><span class="sxs-lookup"><span data-stu-id="98521-177">a.</span></span> <span data-ttu-id="98521-178">Collez la valeur de **	l’URL du service d’authentification unique** dans la zone de texte **URL**.</span><span class="sxs-lookup"><span data-stu-id="98521-178">Paste the **Single Sign-On Service URL** value in to the **URL** textbox.</span></span>
          
    <span data-ttu-id="98521-179">b.</span><span class="sxs-lookup"><span data-stu-id="98521-179">b.</span></span> <span data-ttu-id="98521-180">Ouvrez votre certificat codé en base 64 dans le Bloc-notes, copiez son contenu dans le Presse-papiers, puis collez-le dans la zone de texte **IdP Public Certificate** (Certificat public de fournisseur d’identité).</span><span class="sxs-lookup"><span data-stu-id="98521-180">Open your base-64 encoded certificate in notepad, copy the content of it in to your clipboard, and then paste it to the **IdP Public Certificate** textbox.</span></span>

12. <span data-ttu-id="98521-181">Pour configurer le fournisseur SAML, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="98521-181">To complete the SAML provider configuration, perform the following steps:</span></span>
    
    <span data-ttu-id="98521-182">![Paramètres SAML](./media/active-directory-saas-teamseer-tutorial/ic789638.png "Paramètres SAML")</span><span class="sxs-lookup"><span data-stu-id="98521-182">![SAML Settings](./media/active-directory-saas-teamseer-tutorial/ic789638.png "SAML Settings")</span></span> 

    <span data-ttu-id="98521-183">a.</span><span class="sxs-lookup"><span data-stu-id="98521-183">a.</span></span> <span data-ttu-id="98521-184">Dans la zone de test **Tester l’adresse de messagerie**, entrez l’adresse de messagerie de l’utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="98521-184">In the **Test Email Addresses**, type the test user’s email address.</span></span> 
  
    <span data-ttu-id="98521-185">b.</span><span class="sxs-lookup"><span data-stu-id="98521-185">b.</span></span> <span data-ttu-id="98521-186">Dans la zone de texte **Émetteur** , entrez l’URL de l’émetteur du fournisseur du service.</span><span class="sxs-lookup"><span data-stu-id="98521-186">In the **Issuer** textbox, type the Issuer URL of the service provider.</span></span> 
  
    <span data-ttu-id="98521-187">c.</span><span class="sxs-lookup"><span data-stu-id="98521-187">c.</span></span> <span data-ttu-id="98521-188">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="98521-188">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="98521-189">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="98521-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="98521-190">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="98521-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="98521-191">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="98521-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="98521-192">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="98521-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="98521-193">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="98521-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="98521-195">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="98521-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="98521-196">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="98521-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="98521-198">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="98521-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="98521-200">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="98521-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="98521-202">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="98521-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-teamseer-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="98521-204">a.</span><span class="sxs-lookup"><span data-stu-id="98521-204">a.</span></span> <span data-ttu-id="98521-205">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="98521-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="98521-206">b.</span><span class="sxs-lookup"><span data-stu-id="98521-206">b.</span></span> <span data-ttu-id="98521-207">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="98521-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="98521-208">c.</span><span class="sxs-lookup"><span data-stu-id="98521-208">c.</span></span> <span data-ttu-id="98521-209">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="98521-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="98521-210">d.</span><span class="sxs-lookup"><span data-stu-id="98521-210">d.</span></span> <span data-ttu-id="98521-211">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="98521-211">Click **Create**.</span></span>
 
### <a name="creating-a-teamseer-test-user"></a><span data-ttu-id="98521-212">Création d’un utilisateur de test TeamSeer</span><span class="sxs-lookup"><span data-stu-id="98521-212">Creating a TeamSeer test user</span></span>

<span data-ttu-id="98521-213">Pour se connecter à TeamSeer, les utilisateurs d’Azure AD doivent être approvisionnés dans TeamSeer.</span><span class="sxs-lookup"><span data-stu-id="98521-213">To enable Azure AD users to log in to TeamSeer, they must be provisioned in to ShiftPlanning.</span></span> <span data-ttu-id="98521-214">Dans le cas de TeamSeer, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="98521-214">In the case of TeamSeer, provisioning is a manual task.</span></span>

<span data-ttu-id="98521-215">**Pour approvisionner un compte d’utilisateur, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="98521-215">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="98521-216">Connectez-vous au site d’entreprise **TeamSeer** en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="98521-216">Log in to your **TeamSeer** company site as an administrator.</span></span>

2. <span data-ttu-id="98521-217">Procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="98521-217">Perform the following steps:</span></span>
   
    <span data-ttu-id="98521-218">![Administrateur RH](./media/active-directory-saas-teamseer-tutorial/ic789640.png "Administrateur RH")</span><span class="sxs-lookup"><span data-stu-id="98521-218">![HR Admin](./media/active-directory-saas-teamseer-tutorial/ic789640.png "HR Admin")</span></span>  
 
    <span data-ttu-id="98521-219">a.</span><span class="sxs-lookup"><span data-stu-id="98521-219">a.</span></span> <span data-ttu-id="98521-220">Accédez à **HR Admin \> Users**.</span><span class="sxs-lookup"><span data-stu-id="98521-220">Go to **HR Admin \> Users**.</span></span>
  
    <span data-ttu-id="98521-221">b.</span><span class="sxs-lookup"><span data-stu-id="98521-221">b.</span></span> <span data-ttu-id="98521-222">Cliquez sur **Run the New User wizard**.</span><span class="sxs-lookup"><span data-stu-id="98521-222">Click **Run the New User wizard**.</span></span>

3. <span data-ttu-id="98521-223">Dans la section **User Details** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="98521-223">In the **User Details** section, perform the following steps:</span></span>
   
    <span data-ttu-id="98521-224">![Détails de l’utilisateur](./media/active-directory-saas-teamseer-tutorial/ic789641.png "Détails de l’utilisateur")</span><span class="sxs-lookup"><span data-stu-id="98521-224">![User Details](./media/active-directory-saas-teamseer-tutorial/ic789641.png "User Details")</span></span>

    <span data-ttu-id="98521-225">a.</span><span class="sxs-lookup"><span data-stu-id="98521-225">a.</span></span> <span data-ttu-id="98521-226">Dans les zones de texte correspondantes, indiquez le **prénom**, le **nom** et le **nom d’utilisateur (adresse de messagerie)** d’un compte AAD valide que vous souhaitez approvisionner.</span><span class="sxs-lookup"><span data-stu-id="98521-226">Type the **First Name**, **Surname**, **User name (Email address)** of a valid AAD account you want to provision in to the related textboxes.</span></span>
  
    <span data-ttu-id="98521-227">b.</span><span class="sxs-lookup"><span data-stu-id="98521-227">b.</span></span> <span data-ttu-id="98521-228">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="98521-228">Click **Next**.</span></span>

4. <span data-ttu-id="98521-229">Suivez les instructions à l’écran pour ajouter un nouvel utilisateur, puis cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="98521-229">Follow the on-screen instructions for adding a new user, and click **Finish**.</span></span>

>[!NOTE]
><span data-ttu-id="98521-230">Vous pouvez utiliser n’importe quel outil ou API de création de compte d’utilisateur, fourni par TeamSeer, pour approvisionner des comptes utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="98521-230">You can use any other TeamSeer user account creation tools or APIs provided by TeamSeer to provision Azure AD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="98521-231">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="98521-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="98521-232">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à TeamSeer.</span><span class="sxs-lookup"><span data-stu-id="98521-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TeamSeer.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="98521-234">**Pour affecter Britta Simon à TeamSeer, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="98521-234">**To assign Britta Simon to TeamSeer, perform the following steps:**</span></span>

1. <span data-ttu-id="98521-235">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="98521-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="98521-237">Dans la liste des applications, sélectionnez **TeamSeer**.</span><span class="sxs-lookup"><span data-stu-id="98521-237">In the applications list, select **TeamSeer**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-teamseer-tutorial/tutorial_teamseer_app.png) 

3. <span data-ttu-id="98521-239">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="98521-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="98521-241">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="98521-241">Click **Add** button.</span></span> <span data-ttu-id="98521-242">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="98521-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="98521-244">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="98521-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="98521-245">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="98521-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="98521-246">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="98521-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="98521-247">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="98521-247">Testing single sign-on</span></span>

<span data-ttu-id="98521-248">Si vous souhaitez tester vos paramètres d’authentification unique, ouvrez le volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="98521-248">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="98521-249">Pour plus d'informations sur le panneau d'accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="98521-249">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="98521-250">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="98521-250">Additional resources</span></span>

* [<span data-ttu-id="98521-251">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="98521-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="98521-252">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="98521-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamseer-tutorial/tutorial_general_203.png

