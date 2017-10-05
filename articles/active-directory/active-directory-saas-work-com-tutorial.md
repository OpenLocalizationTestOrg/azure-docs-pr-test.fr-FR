---
title: "Didacticiel : Intégration d’Azure Active Directory à Work.com | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Work.com."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 98e6739e-eb24-46bd-9dd3-20b489839076
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 7cfec8e9ac12d43095483696a15c0580776d3114
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workcom"></a><span data-ttu-id="37a7a-103">Didacticiel : Intégration d’Azure AD à Work.com</span><span class="sxs-lookup"><span data-stu-id="37a7a-103">Tutorial: Azure Active Directory integration with Work.com</span></span>

<span data-ttu-id="37a7a-104">Dans ce didacticiel, vous allez apprendre à intégrer Work.com dans Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="37a7a-104">In this tutorial, you learn how to integrate Work.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="37a7a-105">L’intégration de Work.com dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="37a7a-105">Integrating Work.com with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="37a7a-106">Dans Azure AD, vous pouvez contrôler qui a accès à Work.com.</span><span class="sxs-lookup"><span data-stu-id="37a7a-106">You can control in Azure AD who has access to Work.com</span></span>
- <span data-ttu-id="37a7a-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Work.com (par le biais de l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="37a7a-107">You can enable your users to automatically get signed-on to Work.com (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="37a7a-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="37a7a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="37a7a-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="37a7a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="37a7a-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="37a7a-110">Prerequisites</span></span>

<span data-ttu-id="37a7a-111">Pour configurer l’intégration d’Azure AD à Work.com, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="37a7a-111">To configure Azure AD integration with Work.com, you need the following items:</span></span>

- <span data-ttu-id="37a7a-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="37a7a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="37a7a-113">Un abonnement Work.com pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="37a7a-113">A Work.com single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="37a7a-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="37a7a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="37a7a-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="37a7a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="37a7a-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="37a7a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="37a7a-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="37a7a-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="37a7a-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="37a7a-118">Scenario description</span></span>
<span data-ttu-id="37a7a-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="37a7a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="37a7a-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="37a7a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="37a7a-121">Ajouter Work.com à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="37a7a-121">Add Work.com from the gallery</span></span>
2. <span data-ttu-id="37a7a-122">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="37a7a-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-workcom-from-the-gallery"></a><span data-ttu-id="37a7a-123">Ajouter Work.com à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="37a7a-123">Add Work.com from the gallery</span></span>
<span data-ttu-id="37a7a-124">Pour configurer l’intégration de Work.com à Azure AD, vous devez ajouter Work.com à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="37a7a-124">To configure the integration of Work.com into Azure AD, you need to add Work.com from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="37a7a-125">**Pour ajouter Work.com à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="37a7a-125">**To add Work.com from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="37a7a-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="37a7a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="37a7a-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="37a7a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="37a7a-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="37a7a-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="37a7a-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="37a7a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="37a7a-133">Dans la zone de recherche, tapez **Work.com**, sélectionnez **Work.com** dans le volet de résultats, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="37a7a-133">In the search box, type **Work.com**, select **Work.com** from results panel then click **Add** button to add the application.</span></span>

    ![Ajouter à partir de la galerie](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="37a7a-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="37a7a-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="37a7a-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Work.com avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="37a7a-136">In this section, you configure and test Azure AD single sign-on with Work.com based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="37a7a-137">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Work.com correspondant dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="37a7a-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Work.com is to a user in Azure AD.</span></span> <span data-ttu-id="37a7a-138">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Work.com associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="37a7a-138">In other words, a link relationship between an Azure AD user and the related user in Work.com needs to be established.</span></span>

<span data-ttu-id="37a7a-139">Dans Work.com, assignez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="37a7a-139">In Work.com, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="37a7a-140">Pour configurer et tester l’authentification unique Azure AD avec Work.com, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="37a7a-140">To configure and test Azure AD single sign-on with Work.com, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="37a7a-141">**[Configurer l’authentification unique Azure AD](#configure-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="37a7a-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="37a7a-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="37a7a-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="37a7a-143">**[Créer un utilisateur de test Work.com](#create-a-workcom-test-user)** pour avoir un équivalent de Britta Simon dans Work.com lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="37a7a-143">**[Create a Work.com test user](#create-a-workcom-test-user)** - to have a counterpart of Britta Simon in Work.com that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="37a7a-144">**[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="37a7a-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="37a7a-145">**[Tester l’authentification unique](#test-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="37a7a-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="37a7a-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="37a7a-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="37a7a-147">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Work.com.</span><span class="sxs-lookup"><span data-stu-id="37a7a-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Work.com application.</span></span>

>[!NOTE]
><span data-ttu-id="37a7a-148">Pour configurer l’authentification unique, vous devez encore configurer un nom de domaine personnalisé Work.com.</span><span class="sxs-lookup"><span data-stu-id="37a7a-148">To configure single sign-on, you need to setup a custom Work.com domain name yet.</span></span> <span data-ttu-id="37a7a-149">Vous devez définir au moins un nom de domaine, le tester, puis le déployer dans l’ensemble de votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="37a7a-149">You need to define at least a domain name, test your domain name, and deploy it to your entire organization.</span></span>

<span data-ttu-id="37a7a-150">**Pour configurer l’authentification unique Azure AD avec Work.com, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="37a7a-150">**To configure Azure AD single sign-on with Work.com, perform the following steps:**</span></span>

1. <span data-ttu-id="37a7a-151">Dans le portail Azure, sur la page d’intégration de l’application **Work.com**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="37a7a-151">In the Azure portal, on the **Work.com** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="37a7a-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="37a7a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Authentification basée sur SAML](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_samlbase.png)

3. <span data-ttu-id="37a7a-155">Dans la section **Domaine et URL Work.com**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="37a7a-155">On the **Work.com Domain and URLs** section, perform the following:</span></span>

    ![Section Domaine et URL Work.com](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_url.png)

    <span data-ttu-id="37a7a-157">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `http://<companyname>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="37a7a-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `http://<companyname>.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="37a7a-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="37a7a-158">This value is not real.</span></span> <span data-ttu-id="37a7a-159">Mettez à jour cette valeur avec l’URL de connexion réelle.</span><span class="sxs-lookup"><span data-stu-id="37a7a-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="37a7a-160">Pour obtenir cette valeur, contactez [l’équipe de support technique Work.com](https://help.salesforce.com/articleView?id=000159855&type=3).</span><span class="sxs-lookup"><span data-stu-id="37a7a-160">Contact [Work.com Client support team](https://help.salesforce.com/articleView?id=000159855&type=3) to get this value.</span></span> 

4. <span data-ttu-id="37a7a-161">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="37a7a-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Section Certificat de signature SAML](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_certificate.png) 

5. <span data-ttu-id="37a7a-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="37a7a-163">Click **Save** button.</span></span>

    ![Bouton Enregistrer](./media/active-directory-saas-work-com-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="37a7a-165">Dans la section **Configuration de Work.com**, cliquez sur **Configurer Work.com** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="37a7a-165">On the **Work.com Configuration** section, click **Configure Work.com** to open **Configure sign-on** window.</span></span> <span data-ttu-id="37a7a-166">Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="37a7a-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Section Configuration de Work.com](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_configure.png) 
7. <span data-ttu-id="37a7a-168">Connectez-vous à votre locataire Work.com en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="37a7a-168">Log in to your Work.com tenant as administrator.</span></span>

8. <span data-ttu-id="37a7a-169">Accédez à **Setup**.</span><span class="sxs-lookup"><span data-stu-id="37a7a-169">Go to **Setup**.</span></span>
   
    <span data-ttu-id="37a7a-170">![Configuration](./media/active-directory-saas-work-com-tutorial/ic794108.png "Configuration")</span><span class="sxs-lookup"><span data-stu-id="37a7a-170">![Setup](./media/active-directory-saas-work-com-tutorial/ic794108.png "Setup")</span></span>

9. <span data-ttu-id="37a7a-171">Dans le volet de navigation gauche, dans la section **Administer**, cliquez sur **Domain Management** pour développer la section associée, puis cliquez sur **My Domain** pour ouvrir la page **My Domain**.</span><span class="sxs-lookup"><span data-stu-id="37a7a-171">On the left navigation pane, in the **Administer** section, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span></span> 
   
    <span data-ttu-id="37a7a-172">![Mon domaine](./media/active-directory-saas-work-com-tutorial/ic767825.png "mon domaine")</span><span class="sxs-lookup"><span data-stu-id="37a7a-172">![My Domain](./media/active-directory-saas-work-com-tutorial/ic767825.png "My Domain")</span></span>

10. <span data-ttu-id="37a7a-173">Pour vérifier que votre domaine a été configuré correctement, assurez-vous qu’il figure dans **Step 4 Deployed to Users**, puis passez en revue **My Domain Settings**.</span><span class="sxs-lookup"><span data-stu-id="37a7a-173">To verify that your domain has been set up correctly, make sure that it is in “**Step 4 Deployed to Users**” and review your “**My Domain Settings**”.</span></span>
   
    <span data-ttu-id="37a7a-174">![Domaine déployé sur l’utilisateur](./media/active-directory-saas-work-com-tutorial/ic784377.png "domaine déployé sur l’utilisateur")</span><span class="sxs-lookup"><span data-stu-id="37a7a-174">![Domain Deployed to User](./media/active-directory-saas-work-com-tutorial/ic784377.png "Domain Deployed to User")</span></span>

11. <span data-ttu-id="37a7a-175">Connectez-vous à votre locataire Work.com.</span><span class="sxs-lookup"><span data-stu-id="37a7a-175">Log in to your Work.com tenant.</span></span>

12. <span data-ttu-id="37a7a-176">Accédez à **Setup**.</span><span class="sxs-lookup"><span data-stu-id="37a7a-176">Go to **Setup**.</span></span>
    
    <span data-ttu-id="37a7a-177">![Configuration](./media/active-directory-saas-work-com-tutorial/ic794108.png "Configuration")</span><span class="sxs-lookup"><span data-stu-id="37a7a-177">![Setup](./media/active-directory-saas-work-com-tutorial/ic794108.png "Setup")</span></span>

13. <span data-ttu-id="37a7a-178">Développez le menu **Security Controls**, puis cliquez sur **Single Sign-On Settings**.</span><span class="sxs-lookup"><span data-stu-id="37a7a-178">Expand the **Security Controls** menu, and then click **Single Sign-On Settings**.</span></span>
    
    <span data-ttu-id="37a7a-179">![Paramètres d’authentification unique](./media/active-directory-saas-work-com-tutorial/ic794113.png "paramètres d’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="37a7a-179">![Single Sign-On Settings](./media/active-directory-saas-work-com-tutorial/ic794113.png "Single Sign-On Settings")</span></span>

14. <span data-ttu-id="37a7a-180">Dans la page **Single Sign on Settings** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="37a7a-180">On the **Single Sign-On Settings** dialog page, perform the following steps:</span></span>
    
    <span data-ttu-id="37a7a-181">![SAML activé](./media/active-directory-saas-work-com-tutorial/ic781026.png "SAML activé")</span><span class="sxs-lookup"><span data-stu-id="37a7a-181">![SAML Enabled](./media/active-directory-saas-work-com-tutorial/ic781026.png "SAML Enabled")</span></span>
    
    <span data-ttu-id="37a7a-182">a.</span><span class="sxs-lookup"><span data-stu-id="37a7a-182">a.</span></span> <span data-ttu-id="37a7a-183">Sélectionnez **SAML Enabled**.</span><span class="sxs-lookup"><span data-stu-id="37a7a-183">Select **SAML Enabled**.</span></span>
    
    <span data-ttu-id="37a7a-184">b.</span><span class="sxs-lookup"><span data-stu-id="37a7a-184">b.</span></span> <span data-ttu-id="37a7a-185">Cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="37a7a-185">Click **New**.</span></span>

15. <span data-ttu-id="37a7a-186">Dans la section **SAML Single Sign-On Settings** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="37a7a-186">In the **SAML Single Sign-On Settings** section, perform the following steps:</span></span>
    
    <span data-ttu-id="37a7a-187">![Configuration de l’authentification unique SAML](./media/active-directory-saas-work-com-tutorial/ic794114.png "Configuration de l’authentification unique SAML")</span><span class="sxs-lookup"><span data-stu-id="37a7a-187">![SAML Single Sign-On Setting](./media/active-directory-saas-work-com-tutorial/ic794114.png "SAML Single Sign-On Setting")</span></span>
    
    <span data-ttu-id="37a7a-188">a.</span><span class="sxs-lookup"><span data-stu-id="37a7a-188">a.</span></span> <span data-ttu-id="37a7a-189">Dans la zone de texte **Name** , tapez le nom de votre configuration.</span><span class="sxs-lookup"><span data-stu-id="37a7a-189">In the **Name** textbox, type a name for your configuration.</span></span>  
       
    > [!NOTE]
    > <span data-ttu-id="37a7a-190">Le fait d’entrer une valeur pour **Name** renseigne automatiquement la zone de texte **API Name**.</span><span class="sxs-lookup"><span data-stu-id="37a7a-190">Providing a value for **Name** does automatically populate the **API Name** textbox.</span></span>
    
    <span data-ttu-id="37a7a-191">b.</span><span class="sxs-lookup"><span data-stu-id="37a7a-191">b.</span></span> <span data-ttu-id="37a7a-192">Dans la zone de texte **Émetteur**, collez la valeur de **l’ID d’entité SAML** que vous avez copiée depuis le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="37a7a-192">In **Issuer** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="37a7a-193">c.</span><span class="sxs-lookup"><span data-stu-id="37a7a-193">c.</span></span> <span data-ttu-id="37a7a-194">Pour charger le certificat téléchargé à partir du portail Azure, cliquez sur **Parcourir**.</span><span class="sxs-lookup"><span data-stu-id="37a7a-194">To upload the downloaded certificate from Azure portal, click **Browse**.</span></span>
    
    <span data-ttu-id="37a7a-195">d.</span><span class="sxs-lookup"><span data-stu-id="37a7a-195">d.</span></span> <span data-ttu-id="37a7a-196">Dans la zone de texte **ID d’entité**, tapez `https://salesforce-work.com`.</span><span class="sxs-lookup"><span data-stu-id="37a7a-196">In the **Entity Id** textbox, type `https://salesforce-work.com`.</span></span>
    
    <span data-ttu-id="37a7a-197">e.</span><span class="sxs-lookup"><span data-stu-id="37a7a-197">e.</span></span> <span data-ttu-id="37a7a-198">Pour **SAML Identity Type (Type d’identité SAML)**, sélectionnez **Assertion contains the Federation ID from the User object (L’assertion contient l’ID de fédération de l’objet utilisateur)**.</span><span class="sxs-lookup"><span data-stu-id="37a7a-198">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span></span>
    
    <span data-ttu-id="37a7a-199">f.</span><span class="sxs-lookup"><span data-stu-id="37a7a-199">f.</span></span> <span data-ttu-id="37a7a-200">Pour **SAML Identity Location**, sélectionnez **Identity is in the NameIdentfier element of the Subject statement**.</span><span class="sxs-lookup"><span data-stu-id="37a7a-200">As **SAML Identity Location**, select **Identity is in the NameIdentfier element of the Subject statement**.</span></span>
    
    <span data-ttu-id="37a7a-201">g.</span><span class="sxs-lookup"><span data-stu-id="37a7a-201">g.</span></span> <span data-ttu-id="37a7a-202">Dans la zone de texte **Identity Provider Login URL** (URL de connexion du fournisseur d’identité), collez la valeur de l’**URL du service d’authentification unique SAML** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="37a7a-202">In **Identity Provider Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="37a7a-203">h.</span><span class="sxs-lookup"><span data-stu-id="37a7a-203">h.</span></span> <span data-ttu-id="37a7a-204">Dans la zone de texte **Identity Provider Logout URL** (URL de déconnexion du fournisseur d’identité), collez la valeur de l’**URL de déconnexion** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="37a7a-204">In **Identity Provider Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="37a7a-205">i.</span><span class="sxs-lookup"><span data-stu-id="37a7a-205">i.</span></span> <span data-ttu-id="37a7a-206">Pour **Service Provider Initiated Request Binding**, sélectionnez **HTTP POST**.</span><span class="sxs-lookup"><span data-stu-id="37a7a-206">As **Service Provider Initiated Request Binding**, select **HTTP Post**.</span></span>
    
    <span data-ttu-id="37a7a-207">j.</span><span class="sxs-lookup"><span data-stu-id="37a7a-207">j.</span></span> <span data-ttu-id="37a7a-208">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="37a7a-208">Click **Save**.</span></span>

16. <span data-ttu-id="37a7a-209">Dans le volet de navigation gauche du portail classique Work.com, cliquez sur **Domain Management** pour développer la section associée, puis sur **My Domain** pour ouvrir la page **My Domain**.</span><span class="sxs-lookup"><span data-stu-id="37a7a-209">In your Work.com classic portal, on the left navigation pane, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span></span> 
    
    <span data-ttu-id="37a7a-210">![Mon domaine](./media/active-directory-saas-work-com-tutorial/ic794115.png "mon domaine")</span><span class="sxs-lookup"><span data-stu-id="37a7a-210">![My Domain](./media/active-directory-saas-work-com-tutorial/ic794115.png "My Domain")</span></span>

17. <span data-ttu-id="37a7a-211">Dans la section **Login Page Branding** de la page **My Domain**, cliquez sur **Edit**.</span><span class="sxs-lookup"><span data-stu-id="37a7a-211">On the **My Domain** page, in the **Login Page Branding** section, click **Edit**.</span></span>
    
    <span data-ttu-id="37a7a-212">![Personnalisation de la page de connexion](./media/active-directory-saas-work-com-tutorial/ic767826.png "personnalisation de la page de connexion")</span><span class="sxs-lookup"><span data-stu-id="37a7a-212">![Login Page Branding](./media/active-directory-saas-work-com-tutorial/ic767826.png "Login Page Branding")</span></span>

14. <span data-ttu-id="37a7a-213">Le nom des **SAML SSO Settings** s’affiche dans la section **Authentication Service** de la page **Login Page Branding**.</span><span class="sxs-lookup"><span data-stu-id="37a7a-213">On the **Login Page Branding** page, in the **Authentication Service** section, the name of your **SAML SSO Settings** is displayed.</span></span> <span data-ttu-id="37a7a-214">Sélectionnez-le, puis cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="37a7a-214">Select it, and then click **Save**.</span></span>
    
    <span data-ttu-id="37a7a-215">![Personnalisation de la page de connexion](./media/active-directory-saas-work-com-tutorial/ic784366.png "personnalisation de la page de connexion")</span><span class="sxs-lookup"><span data-stu-id="37a7a-215">![Login Page Branding](./media/active-directory-saas-work-com-tutorial/ic784366.png "Login Page Branding")</span></span>

> [!TIP]
> <span data-ttu-id="37a7a-216">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="37a7a-216">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="37a7a-217">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="37a7a-217">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="37a7a-218">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="37a7a-218">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="37a7a-219">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="37a7a-219">Create an Azure AD test user</span></span>
<span data-ttu-id="37a7a-220">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="37a7a-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="37a7a-222">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="37a7a-222">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="37a7a-223">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="37a7a-223">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-work-com-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="37a7a-225">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="37a7a-225">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Utilisateurs et groupes -> Tous les utilisateurs](./media/active-directory-saas-work-com-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="37a7a-227">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="37a7a-227">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Ajouter](./media/active-directory-saas-work-com-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="37a7a-229">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="37a7a-229">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Boîte de dialogue utilisateur](./media/active-directory-saas-work-com-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="37a7a-231">a.</span><span class="sxs-lookup"><span data-stu-id="37a7a-231">a.</span></span> <span data-ttu-id="37a7a-232">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="37a7a-232">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="37a7a-233">b.</span><span class="sxs-lookup"><span data-stu-id="37a7a-233">b.</span></span> <span data-ttu-id="37a7a-234">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="37a7a-234">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="37a7a-235">c.</span><span class="sxs-lookup"><span data-stu-id="37a7a-235">c.</span></span> <span data-ttu-id="37a7a-236">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="37a7a-236">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="37a7a-237">d.</span><span class="sxs-lookup"><span data-stu-id="37a7a-237">d.</span></span> <span data-ttu-id="37a7a-238">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="37a7a-238">Click **Create**.</span></span>
 
### <a name="create-a-workcom-test-user"></a><span data-ttu-id="37a7a-239">Créer un utilisateur de test Work.com</span><span class="sxs-lookup"><span data-stu-id="37a7a-239">Create a Work.com test user</span></span>
<span data-ttu-id="37a7a-240">Pour que les utilisateurs d’Azure AD puissent se connecter, leur accès doit être approvisionné dans Work.com.</span><span class="sxs-lookup"><span data-stu-id="37a7a-240">For Azure Active Directory users to be able to sign in, they must be provisioned to Work.com.</span></span> <span data-ttu-id="37a7a-241">Dans le cas de Work.com, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="37a7a-241">In the case of Work.com, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="37a7a-242">Pour configurer l'approvisionnement des utilisateurs, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="37a7a-242">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="37a7a-243">Connectez-vous à votre site d’entreprise Work.com en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="37a7a-243">Sign on to your Work.com company site as an administrator.</span></span>

2. <span data-ttu-id="37a7a-244">Accédez à **Setup**.</span><span class="sxs-lookup"><span data-stu-id="37a7a-244">Go to **Setup**.</span></span>
   
    <span data-ttu-id="37a7a-245">![Configuration](./media/active-directory-saas-work-com-tutorial/IC794108.png "Configuration")</span><span class="sxs-lookup"><span data-stu-id="37a7a-245">![Setup](./media/active-directory-saas-work-com-tutorial/IC794108.png "Setup")</span></span>
3. <span data-ttu-id="37a7a-246">Accédez à **Manage Users \> Users**.</span><span class="sxs-lookup"><span data-stu-id="37a7a-246">Go to **Manage Users \> Users**.</span></span>
   
    <span data-ttu-id="37a7a-247">![Gestion des utilisateurs](./media/active-directory-saas-work-com-tutorial/IC784369.png "Gestion des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="37a7a-247">![Manage Users](./media/active-directory-saas-work-com-tutorial/IC784369.png "Manage Users")</span></span>

4. <span data-ttu-id="37a7a-248">Cliquez sur **New User**.</span><span class="sxs-lookup"><span data-stu-id="37a7a-248">Click **New User**.</span></span>
   
    <span data-ttu-id="37a7a-249">![Tous les utilisateurs](./media/active-directory-saas-work-com-tutorial/IC794117.png "Tous les utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="37a7a-249">![All Users](./media/active-directory-saas-work-com-tutorial/IC794117.png "All Users")</span></span>

5. <span data-ttu-id="37a7a-250">Dans la section Modification de l’utilisateur, procédez comme suit pour les attributs d’un compte Azure AD valide que vous souhaitez configurer dans les zones de texte correspondantes :</span><span class="sxs-lookup"><span data-stu-id="37a7a-250">In the User Edit section, perform the following steps, in attributes of a valid Azure AD account you want to provision into the related textboxes:</span></span>
   
    <span data-ttu-id="37a7a-251">![Modification de l’utilisateur](./media/active-directory-saas-work-com-tutorial/ic794118.png "modification de l’utilisateur")</span><span class="sxs-lookup"><span data-stu-id="37a7a-251">![User Edit](./media/active-directory-saas-work-com-tutorial/ic794118.png "User Edit")</span></span>
   
    <span data-ttu-id="37a7a-252">a.</span><span class="sxs-lookup"><span data-stu-id="37a7a-252">a.</span></span> <span data-ttu-id="37a7a-253">Dans la zone de texte **Prénom**, entrez le **prénom** de l’utilisateur **Britta**.</span><span class="sxs-lookup"><span data-stu-id="37a7a-253">In the **First Name** textbox, type the **first name** of the user **Britta**.</span></span>
    
    <span data-ttu-id="37a7a-254">b.</span><span class="sxs-lookup"><span data-stu-id="37a7a-254">b.</span></span> <span data-ttu-id="37a7a-255">Dans la zone de texte **Nom**, entrez le **nom** de l’utilisateur **Simon**.</span><span class="sxs-lookup"><span data-stu-id="37a7a-255">In the **Last Name** textbox, type the **last name** of the user **Simon**.</span></span>
    
    <span data-ttu-id="37a7a-256">c.</span><span class="sxs-lookup"><span data-stu-id="37a7a-256">c.</span></span> <span data-ttu-id="37a7a-257">Dans la zone de texte **Alias**, entrez l’**alias** de l’utilisateur **BrittaS**.</span><span class="sxs-lookup"><span data-stu-id="37a7a-257">In the **Alias** textbox, type the **name** of the user **BrittaS**.</span></span>
    
    <span data-ttu-id="37a7a-258">d.</span><span class="sxs-lookup"><span data-stu-id="37a7a-258">d.</span></span> <span data-ttu-id="37a7a-259">Dans la zone de texte **E-mail**, tapez l’**adresse e-mail** de l’utilisateur, **Brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="37a7a-259">In the **Email** textbox, type the **email address** of user **Brittasimon@contoso.com**.</span></span>
    
    <span data-ttu-id="37a7a-260">e.</span><span class="sxs-lookup"><span data-stu-id="37a7a-260">e.</span></span> <span data-ttu-id="37a7a-261">Dans la zone de texte **Nom d’utilisateur**, entrez un nom d’utilisateur, par exemple **Brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="37a7a-261">In the **User Name** textbox, type a user name of user like **Brittasimon@contoso.com**.</span></span>
    
    <span data-ttu-id="37a7a-262">f.</span><span class="sxs-lookup"><span data-stu-id="37a7a-262">f.</span></span> <span data-ttu-id="37a7a-263">Dans la zone de texte **Surnom**, entrez un **surnom**, par exemple **Simon**.</span><span class="sxs-lookup"><span data-stu-id="37a7a-263">In the **Nick Name** textbox, type a **nick name** of user **Simon**.</span></span>
    
    <span data-ttu-id="37a7a-264">g.</span><span class="sxs-lookup"><span data-stu-id="37a7a-264">g.</span></span> <span data-ttu-id="37a7a-265">Sélectionnez **Rôle**, **Licence utilisateur** et **Profil**.</span><span class="sxs-lookup"><span data-stu-id="37a7a-265">Select **Role**, **User License**, and **Profile**.</span></span>
    
    <span data-ttu-id="37a7a-266">h.</span><span class="sxs-lookup"><span data-stu-id="37a7a-266">h.</span></span> <span data-ttu-id="37a7a-267">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="37a7a-267">Click **Save**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="37a7a-268">Le titulaire du compte Azure AD reçoit alors un message électronique contenant un lien pour confirmer le compte avant qu’il ne soit activé.</span><span class="sxs-lookup"><span data-stu-id="37a7a-268">The Azure AD account holder will get an email including a link to confirm the account before it becomes active.</span></span>
    > 
    > 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="37a7a-269">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="37a7a-269">Assign the Azure AD test user</span></span>

<span data-ttu-id="37a7a-270">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Work.com.</span><span class="sxs-lookup"><span data-stu-id="37a7a-270">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Work.com.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="37a7a-272">**Pour affecter Britta Simon à Work.com, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="37a7a-272">**To assign Britta Simon to Work.com, perform the following steps:**</span></span>

1. <span data-ttu-id="37a7a-273">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="37a7a-273">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="37a7a-275">Dans la liste des applications, sélectionnez **Work.com**.</span><span class="sxs-lookup"><span data-stu-id="37a7a-275">In the applications list, select **Work.com**.</span></span>

    ![Work.com dans la liste des applications](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_app.png) 

3. <span data-ttu-id="37a7a-277">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="37a7a-277">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="37a7a-279">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="37a7a-279">Click **Add** button.</span></span> <span data-ttu-id="37a7a-280">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="37a7a-280">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="37a7a-282">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="37a7a-282">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="37a7a-283">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="37a7a-283">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="37a7a-284">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="37a7a-284">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="37a7a-285">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="37a7a-285">Test single sign-on</span></span>

<span data-ttu-id="37a7a-286">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="37a7a-286">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="37a7a-287">Quand vous cliquez sur la vignette Work.com dans le volet d’accès, vous devez être connecté automatiquement à votre application Work.com.</span><span class="sxs-lookup"><span data-stu-id="37a7a-287">When you click the Work.com tile in the Access Panel, you should get automatically signed-on to your Work.com application.</span></span>
<span data-ttu-id="37a7a-288">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="37a7a-288">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="37a7a-289">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="37a7a-289">Additional resources</span></span>

* [<span data-ttu-id="37a7a-290">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="37a7a-290">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="37a7a-291">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="37a7a-291">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_203.png

