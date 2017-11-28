---
title: "Didacticiel : Intégration d’Azure Active Directory à BenSelect | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et BenSelect."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffa17478-3ea1-4356-a289-545b5b9a4494
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: f8caa023da05863372b7ef92b47a92168445d741
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benselect"></a><span data-ttu-id="2d744-103">Didacticiel : Intégration d'Azure Active Directory à BenSelect</span><span class="sxs-lookup"><span data-stu-id="2d744-103">Tutorial: Azure Active Directory integration with BenSelect</span></span>

<span data-ttu-id="2d744-104">Dans ce didacticiel, vous allez apprendre à intégrer BenSelect à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2d744-104">In this tutorial, you learn how to integrate BenSelect with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2d744-105">L’intégration de BenSelect à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="2d744-105">Integrating BenSelect with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2d744-106">Dans Azure AD, vous pouvez contrôler qui a accès à BenSelect</span><span class="sxs-lookup"><span data-stu-id="2d744-106">You can control in Azure AD who has access to BenSelect</span></span>
- <span data-ttu-id="2d744-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à BenSelect (via l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d744-107">You can enable your users to automatically get signed-on to BenSelect (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2d744-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="2d744-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2d744-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2d744-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2d744-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="2d744-110">Prerequisites</span></span>

<span data-ttu-id="2d744-111">Pour configurer l’intégration d’Azure AD à BenSelect, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="2d744-111">To configure Azure AD integration with BenSelect, you need the following items:</span></span>

- <span data-ttu-id="2d744-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d744-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2d744-113">Un abonnement BenSelect pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="2d744-113">A BenSelect single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2d744-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="2d744-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2d744-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="2d744-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2d744-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="2d744-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2d744-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2d744-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2d744-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="2d744-118">Scenario description</span></span>
<span data-ttu-id="2d744-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="2d744-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2d744-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="2d744-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2d744-121">Ajout de BenSelect à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="2d744-121">Adding BenSelect from the gallery</span></span>
2. <span data-ttu-id="2d744-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d744-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-benselect-from-the-gallery"></a><span data-ttu-id="2d744-123">Ajout de BenSelect à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="2d744-123">Adding BenSelect from the gallery</span></span>
<span data-ttu-id="2d744-124">Pour configurer l’intégration de BenSelect à Azure AD, vous devez ajouter BenSelect à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="2d744-124">To configure the integration of BenSelect into Azure AD, you need to add BenSelect from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2d744-125">**Pour ajouter BenSelect à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2d744-125">**To add BenSelect from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2d744-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2d744-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2d744-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="2d744-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2d744-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="2d744-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="2d744-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="2d744-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="2d744-133">Dans la zone de recherche, tapez **BenSelect**.</span><span class="sxs-lookup"><span data-stu-id="2d744-133">In the search box, type **BenSelect**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_search.png)

5. <span data-ttu-id="2d744-135">Dans le volet de résultats, sélectionnez **BenSelect**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="2d744-135">In the results panel, select **BenSelect**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2d744-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d744-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2d744-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec BenSelect avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="2d744-138">In this section, you configure and test Azure AD single sign-on with BenSelect based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2d744-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur BenSelect équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2d744-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BenSelect is to a user in Azure AD.</span></span> <span data-ttu-id="2d744-140">En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur BenSelect associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="2d744-140">In other words, a link relationship between an Azure AD user and the related user in BenSelect needs to be established.</span></span>

<span data-ttu-id="2d744-141">Dans BenSelect, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="2d744-141">In BenSelect, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="2d744-142">Pour configurer et tester l’authentification unique Azure AD avec BenSelect, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="2d744-142">To configure and test Azure AD single sign-on with BenSelect, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2d744-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="2d744-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="2d744-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2d744-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2d744-145">**[Création d’un utilisateur de test BenSelect](#creating-a-benselect-test-user)** pour avoir un équivalent de Britta Simon dans BenSelect, lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="2d744-145">**[Creating a BenSelect test user](#creating-a-benselect-test-user)** - to have a counterpart of Britta Simon in BenSelect that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="2d744-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2d744-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2d744-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="2d744-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2d744-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d744-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2d744-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application BenSelect.</span><span class="sxs-lookup"><span data-stu-id="2d744-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BenSelect application.</span></span>

<span data-ttu-id="2d744-150">**Pour configurer l’authentification unique Azure AD avec BenSelect, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2d744-150">**To configure Azure AD single sign-on with BenSelect, perform the following steps:**</span></span>

1. <span data-ttu-id="2d744-151">Dans le portail Azure, dans la page d’intégration de l’application **BenSelect**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="2d744-151">In the Azure portal, on the **BenSelect** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="2d744-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="2d744-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_samlbase.png)

3. <span data-ttu-id="2d744-155">Dans la section **Domaine et URL BenSelect**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="2d744-155">On the **BenSelect Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_url.png)

    <span data-ttu-id="2d744-157">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://www.benselect.com/enroll/login.aspx?Path=<tenant name>`</span><span class="sxs-lookup"><span data-stu-id="2d744-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://www.benselect.com/enroll/login.aspx?Path=<tenant name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2d744-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="2d744-158">This value is not real.</span></span> <span data-ttu-id="2d744-159">Mettez à jour la valeur avec l’URL de réponse réelle.</span><span class="sxs-lookup"><span data-stu-id="2d744-159">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="2d744-160">Pour obtenir cette valeur, contactez [l’équipe du support BenSelect](mailto:support@selerix.com).</span><span class="sxs-lookup"><span data-stu-id="2d744-160">Contact [BenSelect support team](mailto:support@selerix.com) to get this value.</span></span>
 
4. <span data-ttu-id="2d744-161">Dans la section **Certificat de signature SAML**, cliquez sur **Certificat (brut)**, puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="2d744-161">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_certificate.png) 

5. <span data-ttu-id="2d744-163">L’application BenSelect attend les assertions SAML dans un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="2d744-163">BenSelect application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="2d744-164">Configurez les revendications suivantes pour cette application.</span><span class="sxs-lookup"><span data-stu-id="2d744-164">Configure the following claims for this application.</span></span> <span data-ttu-id="2d744-165">Vous pouvez gérer les valeurs de ces attributs à partir de la section **Attributs utilisateur** sur la page d’intégration des applications.</span><span class="sxs-lookup"><span data-stu-id="2d744-165">You can manage the values of these attributes from the **User Attributes** section on application integration page.</span></span> <span data-ttu-id="2d744-166">La capture d’écran suivante montre un exemple :</span><span class="sxs-lookup"><span data-stu-id="2d744-166">The following screenshot shows an example for this.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_06.png)

6. <span data-ttu-id="2d744-168">Dans la section **Attributs utilisateur** de la boîte de dialogue **Authentification unique** :</span><span class="sxs-lookup"><span data-stu-id="2d744-168">In the **User Attributes** section on the **Single sign-on** dialog:</span></span>

    <span data-ttu-id="2d744-169">a.</span><span class="sxs-lookup"><span data-stu-id="2d744-169">a.</span></span> <span data-ttu-id="2d744-170">Dans la liste déroulante **Identificateur de l’utilisateur**, sélectionnez **ExtractMailPrefix**.</span><span class="sxs-lookup"><span data-stu-id="2d744-170">In the **User Identifier** dropdown list, select **ExtractMailPrefix**.</span></span>

    <span data-ttu-id="2d744-171">b.</span><span class="sxs-lookup"><span data-stu-id="2d744-171">b.</span></span> <span data-ttu-id="2d744-172">Dans la liste déroulante **E-mail**, sélectionnez **user.userprincipalname**.</span><span class="sxs-lookup"><span data-stu-id="2d744-172">In the **Mail** dropdown list, select **user.userprincipalname**.</span></span>

7. <span data-ttu-id="2d744-173">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="2d744-173">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-benselect-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="2d744-175">Dans la section **Configuration de BenSelect**, cliquez sur **Configurer BenSelect** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="2d744-175">On the **BenSelect Configuration** section, click **Configure BenSelect** to open **Configure sign-on** window.</span></span> <span data-ttu-id="2d744-176">Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="2d744-176">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_configure.png) 

9. <span data-ttu-id="2d744-178">Pour configurer l’authentification unique côté **BenSelect**, vous devez envoyer le **Certificat (brut)** téléchargé et **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à [l’équipe du support BenSelect](mailto:support@selerix.com).</span><span class="sxs-lookup"><span data-stu-id="2d744-178">To configure single sign-on on **BenSelect** side, you need to send the downloaded **Certificate(Raw)** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [BenSelect support team](mailto:support@selerix.com).</span></span>

   >[!NOTE]
   ><span data-ttu-id="2d744-179">Vous devez indiquer que cette intégration nécessite l’algorithme SHA256 (SHA1 n’est pas pris en charge) pour définir l’authentification unique sur le serveur approprié, comme app2101, etc.</span><span class="sxs-lookup"><span data-stu-id="2d744-179">You need to mention that this integration requires the SHA256 algorithm (SHA1 is not supported) to set the SSO on the appropriate server like app2101 etc.</span></span> 
   
> [!TIP]
> <span data-ttu-id="2d744-180">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="2d744-180">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2d744-181">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="2d744-181">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2d744-182">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2d744-182">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2d744-183">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d744-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="2d744-184">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2d744-184">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="2d744-186">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2d744-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2d744-187">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2d744-187">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-benselect-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2d744-189">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="2d744-189">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-benselect-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2d744-191">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="2d744-191">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-benselect-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2d744-193">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="2d744-193">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-benselect-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2d744-195">a.</span><span class="sxs-lookup"><span data-stu-id="2d744-195">a.</span></span> <span data-ttu-id="2d744-196">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2d744-196">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2d744-197">b.</span><span class="sxs-lookup"><span data-stu-id="2d744-197">b.</span></span> <span data-ttu-id="2d744-198">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2d744-198">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2d744-199">c.</span><span class="sxs-lookup"><span data-stu-id="2d744-199">c.</span></span> <span data-ttu-id="2d744-200">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="2d744-200">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2d744-201">d.</span><span class="sxs-lookup"><span data-stu-id="2d744-201">d.</span></span> <span data-ttu-id="2d744-202">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="2d744-202">Click **Create**.</span></span>
 
### <a name="creating-a-benselect-test-user"></a><span data-ttu-id="2d744-203">Création d’un utilisateur test BenSelect</span><span class="sxs-lookup"><span data-stu-id="2d744-203">Creating a BenSelect test user</span></span>

<span data-ttu-id="2d744-204">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans BenSelect.</span><span class="sxs-lookup"><span data-stu-id="2d744-204">The objective of this section is to create a user called Britta Simon in BenSelect.</span></span> <span data-ttu-id="2d744-205">Pour ajouter des utilisateurs dans le compte BenSelect, contactez [l’équipe du support BenSelect](mailto:support@selerix.com).</span><span class="sxs-lookup"><span data-stu-id="2d744-205">Work with [BenSelect support team](mailto:support@selerix.com) to add the users in the BenSelect account.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2d744-206">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="2d744-206">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2d744-207">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à BenSelect.</span><span class="sxs-lookup"><span data-stu-id="2d744-207">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BenSelect.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="2d744-209">**Pour affecter Britta Simon à BenSelect, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2d744-209">**To assign Britta Simon to BenSelect, perform the following steps:**</span></span>

1. <span data-ttu-id="2d744-210">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="2d744-210">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="2d744-212">Dans la liste des applications, sélectionnez **BenSelect**.</span><span class="sxs-lookup"><span data-stu-id="2d744-212">In the applications list, select **BenSelect**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-benselect-tutorial/tutorial_benselect_app.png) 

3. <span data-ttu-id="2d744-214">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="2d744-214">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="2d744-216">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="2d744-216">Click **Add** button.</span></span> <span data-ttu-id="2d744-217">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="2d744-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="2d744-219">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="2d744-219">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="2d744-220">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="2d744-220">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2d744-221">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="2d744-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2d744-222">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="2d744-222">Testing single sign-on</span></span>

<span data-ttu-id="2d744-223">Dans cette section, vous allez tester la configuration SSO Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="2d744-223">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="2d744-224">Quand vous cliquez sur la vignette BenSelect dans le volet d’accès, vous devez être connecté automatiquement à votre application BenSelect.</span><span class="sxs-lookup"><span data-stu-id="2d744-224">When you click the BenSelect tile in the Access Panel, you should get automatically signed-on to your BenSelect application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2d744-225">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="2d744-225">Additional resources</span></span>

* [<span data-ttu-id="2d744-226">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2d744-226">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2d744-227">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="2d744-227">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-benselect-tutorial/tutorial_general_203.png

