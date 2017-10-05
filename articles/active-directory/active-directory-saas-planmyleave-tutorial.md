---
title: "Didacticiel : Intégration d’Azure Active Directory à PlanMyLeave | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et PlanMyLeave."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b0d31cbe-7ae2-488b-9cf3-4927391fa744
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: jeedes
ms.openlocfilehash: ba418a641b339a0d94a3c7b2596d37fbd88a30c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-planmyleave"></a><span data-ttu-id="836a8-103">Didacticiel : Intégration de PlanMyLeave à Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="836a8-103">Tutorial: Azure Active Directory integration with PlanMyLeave</span></span>

<span data-ttu-id="836a8-104">Dans ce didacticiel, vous allez apprendre à intégrer PlanMyLeave à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="836a8-104">In this tutorial, you learn how to integrate PlanMyLeave with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="836a8-105">L’intégration de PlanMyLeave à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="836a8-105">Integrating PlanMyLeave with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="836a8-106">Dans Azure AD, vous pouvez contrôler qui a accès à PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="836a8-106">You can control in Azure AD who has access to PlanMyLeave</span></span>
- <span data-ttu-id="836a8-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à PlanMyLeave (par le biais de l’authentification unique) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="836a8-107">You can enable your users to automatically get signed-on to PlanMyLeave (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="836a8-108">Vous pouvez gérer vos comptes de manière centralisée dans le portail de gestion Azure.</span><span class="sxs-lookup"><span data-stu-id="836a8-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="836a8-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="836a8-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="836a8-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="836a8-110">Prerequisites</span></span>

<span data-ttu-id="836a8-111">Pour configurer l’intégration d’Azure AD dans PlanMyLeave, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="836a8-111">To configure Azure AD integration with PlanMyLeave, you need the following items:</span></span>

- <span data-ttu-id="836a8-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="836a8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="836a8-113">Un abonnement PlanMyLeave pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="836a8-113">A PlanMyLeave single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="836a8-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="836a8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="836a8-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="836a8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="836a8-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="836a8-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="836a8-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="836a8-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="836a8-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="836a8-118">Scenario description</span></span>
<span data-ttu-id="836a8-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="836a8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="836a8-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="836a8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="836a8-121">Ajout de PlanMyLeave depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="836a8-121">Adding PlanMyLeave from the gallery</span></span>
2. <span data-ttu-id="836a8-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="836a8-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-planmyleave-from-the-gallery"></a><span data-ttu-id="836a8-123">Ajout de PlanMyLeave depuis la galerie</span><span class="sxs-lookup"><span data-stu-id="836a8-123">Adding PlanMyLeave from the gallery</span></span>
<span data-ttu-id="836a8-124">Pour configurer l’intégration de PlanMyLeave à Azure AD, vous devez ajouter PlanMyLeave depuis la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="836a8-124">To configure the integration of PlanMyLeave into Azure AD, you need to add PlanMyLeave from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="836a8-125">**Pour ajouter PlanMyLeave à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="836a8-125">**To add PlanMyLeave from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="836a8-126">Dans le panneau de navigation gauche du **[Portail de gestion Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="836a8-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="836a8-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="836a8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="836a8-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="836a8-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="836a8-131">Cliquez sur le bouton **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="836a8-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="836a8-133">Dans le champ de recherche, entrez **PlanMyLeave**.</span><span class="sxs-lookup"><span data-stu-id="836a8-133">In the search box, type **PlanMyLeave**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_001.png)

5. <span data-ttu-id="836a8-135">Dans le volet de résultats, sélectionnez **PlanMyLeave**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="836a8-135">In the results panel, select **PlanMyLeave**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="836a8-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="836a8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="836a8-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec PlanMyLeave avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="836a8-138">In this section, you configure and test Azure AD single sign-on with PlanMyLeave based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="836a8-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur PlanMyLeave équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="836a8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in PlanMyLeave is to a user in Azure AD.</span></span> <span data-ttu-id="836a8-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur PlanMyLeave associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="836a8-140">In other words, a link relationship between an Azure AD user and the related user in PlanMyLeave needs to be established.</span></span>

<span data-ttu-id="836a8-141">Pour cela, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** dans PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="836a8-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in PlanMyLeave.</span></span>

<span data-ttu-id="836a8-142">Pour configurer et tester l’authentification unique Azure AD avec PlanMyLeave, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="836a8-142">To configure and test Azure AD single sign-on with PlanMyLeave, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="836a8-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="836a8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="836a8-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="836a8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="836a8-145">**[Création d’un utilisateur de test PlanMyLeave](#creating-a-planmyleave-test-user)** pour avoir un équivalent de Britta Simon dans PlanMyLeave qui soit lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="836a8-145">**[Creating a PlanMyLeave test user](#creating-a-planmyleave-test-user)** - to have a counterpart of Britta Simon in PlanMyLeave that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="836a8-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="836a8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="836a8-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="836a8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="836a8-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="836a8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="836a8-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail de gestion Azure et configurer l’authentification unique dans votre application PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="836a8-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your PlanMyLeave application.</span></span>

<span data-ttu-id="836a8-150">**Pour configurer l’authentification unique Azure AD avec PlanMyLeave, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="836a8-150">**To configure Azure AD single sign-on with PlanMyLeave, perform the following steps:**</span></span>

1. <span data-ttu-id="836a8-151">Dans le portail de gestion Azure, sur la page d’intégration de l’application **PlanMyLeave**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="836a8-151">In the Azure Management portal, on the **PlanMyLeave** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="836a8-153">Dans la boîte de dialogue **Authentification unique**, sous **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="836a8-153">On the **Single sign-on** dialog page, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_01.png)

3. <span data-ttu-id="836a8-155">Dans la section **Domaine et URL PlanMyLeave**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="836a8-155">On the **PlanMyLeave Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_02.png)

    <span data-ttu-id="836a8-157">a.</span><span class="sxs-lookup"><span data-stu-id="836a8-157">a.</span></span> <span data-ttu-id="836a8-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<company-name>.planmyleave.com/Login.aspx`</span><span class="sxs-lookup"><span data-stu-id="836a8-158">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<company-name>.planmyleave.com/Login.aspx`</span></span>
    
    <span data-ttu-id="836a8-159">b.</span><span class="sxs-lookup"><span data-stu-id="836a8-159">b.</span></span> <span data-ttu-id="836a8-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<company-name>.planmyleave.com`</span><span class="sxs-lookup"><span data-stu-id="836a8-160">In the **Identifer** textbox, type a URL using the following pattern: `https://<company-name>.planmyleave.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="836a8-161">Notez qu’il ne s’agit pas des valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="836a8-161">Please note that these are not the real values.</span></span> <span data-ttu-id="836a8-162">Vous devez mettre à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="836a8-162">You have to update these values with the actual Sign On URL and Identifier.</span></span> <span data-ttu-id="836a8-163">Contactez [l’équipe de support technique PlanMyLeave](mailto:support@planmyleave.com) pour obtenir ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="836a8-163">Contact [PlanMyLeave support team](mailto:support@planmyleave.com) to get these values.</span></span>

4. <span data-ttu-id="836a8-164">Dans la section **Certificat de signature SAML**, cliquez sur **Créer un certificat**.</span><span class="sxs-lookup"><span data-stu-id="836a8-164">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_03.png)     

5. <span data-ttu-id="836a8-166">Dans la boîte de dialogue **Créer un certificat**, cliquez sur l’icône de calendrier et sélectionnez une **date d’expiration**.</span><span class="sxs-lookup"><span data-stu-id="836a8-166">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="836a8-167">Ensuite, cliquez sur le bouton **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="836a8-167">Then click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="836a8-169">Dans la section **Certificat de signature SAML**, sélectionnez **Activer le nouveau certificat** et cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="836a8-169">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_04.png)

7. <span data-ttu-id="836a8-171">Dans la fenêtre contextuelle **Certificat de substitution**, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="836a8-171">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="836a8-173">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="836a8-173">On the **SAML Signing Certificate** section, click **Certificate (base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_05.png) 

9. <span data-ttu-id="836a8-175">Dans la section **Configuration de PlanMyLeave** , cliquez sur **Configurer PlanMyLeave** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="836a8-175">On the **PlanMyLeave Configuration** section, click **Configure PlanMyLeave** to open **Configure sign-on** window.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_06.png) 

    ![Configurer l’authentification unique](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_07.png)

10. <span data-ttu-id="836a8-178">Dans une autre fenêtre de navigateur web, connectez-vous à votre locataire PlanMyLeave en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="836a8-178">In a different web browser window, log into your PlanMyLeave tenant as an administrator.</span></span>

11. <span data-ttu-id="836a8-179">Accédez à la section **System Setup** (Configuration système).</span><span class="sxs-lookup"><span data-stu-id="836a8-179">Go to **System Setup**.</span></span> <span data-ttu-id="836a8-180">Puis, dans la section **Security Management** (Gestion de la sécurité), cliquez sur **Company SAML settings** (Paramètres SAML d’entreprise).</span><span class="sxs-lookup"><span data-stu-id="836a8-180">Then on the **Security Management** section click **Company SAML settings** .</span></span>

    ![Configurer l’authentification unique côté application](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_002.png) 

12. <span data-ttu-id="836a8-182">Dans la section **SAML Settings** (Paramètres SAML), cliquez sur icône de l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="836a8-182">On the **SAML Settings** section, click editor icon.</span></span>

    ![Configurer l’authentification unique côté application](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_003.png)

13. <span data-ttu-id="836a8-184">Dans la section **Update SAML Settings** (Mettre à jour les paramètres SAML), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="836a8-184">On the **Update SAML Settings** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique côté application](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_004.png)

    <span data-ttu-id="836a8-186">a.</span><span class="sxs-lookup"><span data-stu-id="836a8-186">a.</span></span>  <span data-ttu-id="836a8-187">Dans la zone de texte **Login URL** (URL de connexion), copiez la valeur de **URL du service d’authentification unique SAML** indiquée dans la fenêtre Configuration de l’application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="836a8-187">In the **Login URL** textbox, put the value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span></span>

    <span data-ttu-id="836a8-188">b.</span><span class="sxs-lookup"><span data-stu-id="836a8-188">b.</span></span>  <span data-ttu-id="836a8-189">Ouvrez votre fichier de certificat téléchargé dans le Bloc-notes, copiez uniquement le contenu compris entre ---Begin Certificate--- et ---End certificate---- dans le Presse-papiers, puis collez-le dans la zone de texte **Certificat**.</span><span class="sxs-lookup"><span data-stu-id="836a8-189">Open your downloaded certificate file in notepad, copy only the content between the ---Begin Certificate--- and ---End certificate---- of it into your clipboard, and then paste it to the **Certificate** textbox.</span></span>

    <span data-ttu-id="836a8-190">c.</span><span class="sxs-lookup"><span data-stu-id="836a8-190">c.</span></span> <span data-ttu-id="836a8-191">Définissez "**Is Enable**" sur "**Yes**".</span><span class="sxs-lookup"><span data-stu-id="836a8-191">Set "**Is Enable**" to "**Yes**".</span></span>

    <span data-ttu-id="836a8-192">d.</span><span class="sxs-lookup"><span data-stu-id="836a8-192">d.</span></span> <span data-ttu-id="836a8-193">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="836a8-193">Click **Save**.</span></span>



### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="836a8-194">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="836a8-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="836a8-195">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le Portail de gestion Azure.</span><span class="sxs-lookup"><span data-stu-id="836a8-195">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="836a8-197">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="836a8-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="836a8-198">Dans le panneau de navigation gauche du **Portail de gestion Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="836a8-198">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="836a8-200">Accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs** pour afficher la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="836a8-200">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="836a8-202">En haut de la boîte de dialogue, cliquez sur **Ajouter** pour ouvrir la boîte de dialogue **Utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="836a8-202">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="836a8-204">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="836a8-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="836a8-206">a.</span><span class="sxs-lookup"><span data-stu-id="836a8-206">a.</span></span> <span data-ttu-id="836a8-207">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="836a8-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="836a8-208">b.</span><span class="sxs-lookup"><span data-stu-id="836a8-208">b.</span></span> <span data-ttu-id="836a8-209">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="836a8-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="836a8-210">c.</span><span class="sxs-lookup"><span data-stu-id="836a8-210">c.</span></span> <span data-ttu-id="836a8-211">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="836a8-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="836a8-212">d.</span><span class="sxs-lookup"><span data-stu-id="836a8-212">d.</span></span> <span data-ttu-id="836a8-213">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="836a8-213">Click **Create**.</span></span> 



### <a name="creating-a-planmyleave-test-user"></a><span data-ttu-id="836a8-214">Création d’un utilisateur de test PlanMyLeave</span><span class="sxs-lookup"><span data-stu-id="836a8-214">Creating a PlanMyLeave test user</span></span>

<span data-ttu-id="836a8-215">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="836a8-215">The objective of this section is to create a user called Britta Simon in PlanMyLeave.</span></span> <span data-ttu-id="836a8-216">PlanMyLeave prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="836a8-216">PlanMyLeave supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="836a8-217">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="836a8-217">There is no action item for you in this section.</span></span> <span data-ttu-id="836a8-218">Un utilisateur est créé lors d’une tentative d’accès à PlanMyLeave s’il n’existe pas déjà.</span><span class="sxs-lookup"><span data-stu-id="836a8-218">A new user will be created during an attempt to access PlanMyLeave if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="836a8-219">Si vous devez créer un utilisateur manuellement, contactez l’[équipe du support technique PlanMyLeave](mailto:support@planmyleave.com).</span><span class="sxs-lookup"><span data-stu-id="836a8-219">If you need to create an user manually, you need to contact [PlanMyLeave support team](mailto:support@planmyleave.com).</span></span>



### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="836a8-220">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="836a8-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="836a8-221">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="836a8-221">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to PlanMyLeave.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="836a8-223">**Pour affecter Britta Simon à PlanMyLeave, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="836a8-223">**To assign Britta Simon to PlanMyLeave, perform the following steps:**</span></span>

1. <span data-ttu-id="836a8-224">Dans le Portail de gestion Azure, ouvrez la vue des applications, accédez à la vue des répertoires, allez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="836a8-224">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="836a8-226">Dans la liste des applications, sélectionnez **PlanMyLeave**.</span><span class="sxs-lookup"><span data-stu-id="836a8-226">In the applications list, select **PlanMyLeave**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_50.png) 

3. <span data-ttu-id="836a8-228">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="836a8-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="836a8-230">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="836a8-230">Click **Add** button.</span></span> <span data-ttu-id="836a8-231">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="836a8-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="836a8-233">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="836a8-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="836a8-234">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="836a8-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="836a8-235">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="836a8-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="836a8-236">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="836a8-236">Testing single sign-on</span></span>

<span data-ttu-id="836a8-237">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="836a8-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="836a8-238">Quand vous cliquez sur la vignette PlanMyLeave dans le volet d’accès, vous êtes connecté automatiquement à votre application PlanMyLeave.</span><span class="sxs-lookup"><span data-stu-id="836a8-238">When you click the PlanMyLeave tile in the Access Panel, you should get automatically signed-on to your PlanMyLeave application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="836a8-239">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="836a8-239">Additional resources</span></span>

* [<span data-ttu-id="836a8-240">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="836a8-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="836a8-241">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="836a8-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_203.png