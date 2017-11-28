---
title: "Tutorial: Intégration d'Azure Active Directory à Box | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Box."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5f3517f8-30f2-4be7-9e47-43d702701797
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 2cc2afe8ff3f0063224c94eb0b8135347051b0aa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-box"></a><span data-ttu-id="ddfc1-103">Didacticiel : Intégration d'Azure Active Directory à Box</span><span class="sxs-lookup"><span data-stu-id="ddfc1-103">Tutorial: Azure Active Directory integration with Box</span></span>

<span data-ttu-id="ddfc1-104">Dans ce didacticiel, vous allez apprendre à intégrer Box dans Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ddfc1-104">In this tutorial, you learn how to integrate Box with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ddfc1-105">L’intégration de Box dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="ddfc1-105">Integrating Box with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ddfc1-106">Dans Azure AD, vous pouvez contrôler qui a accès à Box</span><span class="sxs-lookup"><span data-stu-id="ddfc1-106">You can control in Azure AD who has access to Box</span></span>
- <span data-ttu-id="ddfc1-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Box (par authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-107">You can enable your users to automatically get signed-on to Box (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ddfc1-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="ddfc1-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ddfc1-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ddfc1-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ddfc1-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ddfc1-110">Prerequisites</span></span>

<span data-ttu-id="ddfc1-111">Pour configurer l’intégration d’Azure AD à Box, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="ddfc1-111">To configure Azure AD integration with Box, you need the following items:</span></span>

- <span data-ttu-id="ddfc1-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="ddfc1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ddfc1-113">Un abonnement Box pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="ddfc1-113">A Box single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ddfc1-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ddfc1-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ddfc1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ddfc1-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ddfc1-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ddfc1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ddfc1-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="ddfc1-118">Scenario description</span></span>
<span data-ttu-id="ddfc1-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ddfc1-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="ddfc1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ddfc1-121">Ajout de Box à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="ddfc1-121">Adding Box from the gallery</span></span>
2. <span data-ttu-id="ddfc1-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ddfc1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-box-from-the-gallery"></a><span data-ttu-id="ddfc1-123">Ajout de Box à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="ddfc1-123">Adding Box from the gallery</span></span>
<span data-ttu-id="ddfc1-124">Pour configurer l’intégration de Box à Azure AD, vous devez ajouter Box, disponible dans la galerie, à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-124">To configure the integration of Box into Azure AD, you need to add Box from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ddfc1-125">**Pour ajouter Box à partir de la galerie, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="ddfc1-125">**To add Box from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ddfc1-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ddfc1-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ddfc1-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="ddfc1-131">Cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-131">Click **New application** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="ddfc1-133">Dans la zone de recherche, tapez **Box**.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-133">In the search box, type **Box**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-box-tutorial/tutorial_box_search.png)

5. <span data-ttu-id="ddfc1-135">Dans le volet de résultats, sélectionnez **Box**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-135">In the results panel, select **Box**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-box-tutorial/tutorial_box_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ddfc1-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ddfc1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ddfc1-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Box, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="ddfc1-138">In this section, you configure and test Azure AD single sign-on with Box based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ddfc1-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Box correspondant dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Box is to a user in Azure AD.</span></span> <span data-ttu-id="ddfc1-140">En d’autres termes, une relation doit être établie entre l’utilisateur Azure AD et l’utilisateur Box associé.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-140">In other words, a link relationship between an Azure AD user and the related user in Box needs to be established.</span></span>

<span data-ttu-id="ddfc1-141">Pour cela, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** dans Box.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Box.</span></span>

<span data-ttu-id="ddfc1-142">Pour configurer et tester l’authentification unique Azure AD avec Box, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="ddfc1-142">To configure and test Azure AD single sign-on with Box, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ddfc1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ddfc1-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ddfc1-145">**[Création d’un utilisateur de test Box](#creating-a-box-test-user)** pour avoir un équivalent de Britta Simon dans Box lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-145">**[Creating a Box test user](#creating-a-box-test-user)** - to have a counterpart of Britta Simon in Box that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ddfc1-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ddfc1-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ddfc1-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ddfc1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ddfc1-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Box.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Box application.</span></span>

<span data-ttu-id="ddfc1-150">**Pour configurer l’authentification unique Azure AD avec Box, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="ddfc1-150">**To configure Azure AD single sign-on with Box, perform the following steps:**</span></span>

1. <span data-ttu-id="ddfc1-151">Dans le portail Azure, dans la page d’intégration de l’application **Box**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-151">In the Azure portal, on the **Box** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="ddfc1-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-box-tutorial/tutorial_box_samlbase.png)

3. <span data-ttu-id="ddfc1-155">Dans la section **Domaine et URL Box**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="ddfc1-155">On the **Box Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-box-tutorial/tutorial_box_url.png)

    <span data-ttu-id="ddfc1-157">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<subdomain>.box.com`</span><span class="sxs-lookup"><span data-stu-id="ddfc1-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.box.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ddfc1-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-158">This value is not real.</span></span> <span data-ttu-id="ddfc1-159">Mettez à jour la valeur avec l’URL de connexion réelle.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-159">Update the value with the actual Sign-on URL.</span></span> <span data-ttu-id="ddfc1-160">Pour obtenir cette valeur, contactez [l’équipe du support Box](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire).</span><span class="sxs-lookup"><span data-stu-id="ddfc1-160">Contact [Box Client support team](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) to get this value.</span></span> 
 
4. <span data-ttu-id="ddfc1-161">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier XML sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-box-tutorial/tutorial_box_certificate.png) 

5. <span data-ttu-id="ddfc1-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="ddfc1-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-box-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ddfc1-165">Pour configurer l’authentification unique dans votre application, contactez [l’équipe du support Box](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) en lui fournissant le fichier XML téléchargé.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-165">To get SSO configured for your application, Contact [Box Client support team](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) and provide them with the downloaded XML file.</span></span>

> [!TIP]
> <span data-ttu-id="ddfc1-166">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-166">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ddfc1-167">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-167">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ddfc1-168">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ddfc1-168">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ddfc1-169">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="ddfc1-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="ddfc1-170">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="ddfc1-172">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ddfc1-172">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ddfc1-173">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-173">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-box-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ddfc1-175">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-175">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-box-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ddfc1-177">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-177">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-box-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ddfc1-179">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="ddfc1-179">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-box-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ddfc1-181">a.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-181">a.</span></span> <span data-ttu-id="ddfc1-182">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-182">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ddfc1-183">b.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-183">b.</span></span> <span data-ttu-id="ddfc1-184">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-184">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ddfc1-185">c.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-185">c.</span></span> <span data-ttu-id="ddfc1-186">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-186">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ddfc1-187">d.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-187">d.</span></span> <span data-ttu-id="ddfc1-188">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-188">Click **Create**.</span></span>
 
### <a name="creating-a-box-test-user"></a><span data-ttu-id="ddfc1-189">Création d’un utilisateur de test Box</span><span class="sxs-lookup"><span data-stu-id="ddfc1-189">Creating a Box test user</span></span>

<span data-ttu-id="ddfc1-190">Dans cette section, un utilisateur appelé Britta Simon est créé dans Box.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-190">In this section, a user called Britta Simon is created in Box.</span></span> <span data-ttu-id="ddfc1-191">Box prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-191">Box supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="ddfc1-192">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-192">There is no action item for you in this section.</span></span> <span data-ttu-id="ddfc1-193">S’il n’y a pas déjà un utilisateur dans Box, un nouvel utilisateur est créé lorsque vous tentez d’y accéder.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-193">If a user doesn't already exist in Box, a new one is created when you attempt to access Box.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ddfc1-194">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="ddfc1-194">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ddfc1-195">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Box.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Box.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="ddfc1-197">**Pour attribuer Britta Simon à Box, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="ddfc1-197">**To assign Britta Simon to Box, perform the following steps:**</span></span>

1. <span data-ttu-id="ddfc1-198">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="ddfc1-200">Dans la liste des applications, sélectionnez **Box**.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-200">In the applications list, select **Box**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-box-tutorial/tutorial_box_app.png) 

3. <span data-ttu-id="ddfc1-202">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-202">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="ddfc1-204">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-204">Click **Add** button.</span></span> <span data-ttu-id="ddfc1-205">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="ddfc1-207">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ddfc1-208">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ddfc1-209">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ddfc1-210">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="ddfc1-210">Testing single sign-on</span></span>

<span data-ttu-id="ddfc1-211">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-211">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ddfc1-212">Le fait de cliquer sur la vignette Box dans le volet d’accès vous connecte automatiquement à votre application Box.</span><span class="sxs-lookup"><span data-stu-id="ddfc1-212">When you click the Box tile in the Access Panel, you should get login page to get signed-on to your Box application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ddfc1-213">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="ddfc1-213">Additional resources</span></span>

* [<span data-ttu-id="ddfc1-214">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ddfc1-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ddfc1-215">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="ddfc1-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="ddfc1-216">Configurer l’approvisionnement de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="ddfc1-216">Configure User Provisioning</span></span>](active-directory-saas-box-userprovisioning-tutorial.md)


<!--Image references-->

[1]: ./media/active-directory-saas-box-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-box-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-box-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-box-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-box-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-box-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-box-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-box-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-box-tutorial/tutorial_general_203.png

