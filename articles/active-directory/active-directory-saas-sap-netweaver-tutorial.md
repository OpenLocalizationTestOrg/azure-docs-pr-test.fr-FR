---
title: "Didacticiel : Intégration d’Azure Active Directory à SAP NetWeaver | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et SAP NetWeaver."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1b9e59e3-e7ae-4e74-b16c-8c1a7ccfdef3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: ad4140eb1183094a67822ad92eabcd35101360b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-netweaver"></a><span data-ttu-id="398e3-103">Didacticiel : Intégration d’Azure Active Directory à SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="398e3-103">Tutorial: Azure Active Directory integration with SAP NetWeaver</span></span>

<span data-ttu-id="398e3-104">Dans ce didacticiel, vous allez apprendre à intégrer SAP NetWeaver à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="398e3-104">In this tutorial, you learn how to integrate SAP NetWeaver with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="398e3-105">L’intégration de SAP NetWeaver à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="398e3-105">Integrating SAP NetWeaver with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="398e3-106">Dans Azure AD, vous pouvez contrôler qui a accès à SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="398e3-106">You can control in Azure AD who has access to SAP NetWeaver</span></span>
- <span data-ttu-id="398e3-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à SAP NetWeaver (via l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="398e3-107">You can enable your users to automatically get signed-on to SAP NetWeaver (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="398e3-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="398e3-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="398e3-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="398e3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="398e3-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="398e3-110">Prerequisites</span></span>

<span data-ttu-id="398e3-111">Pour configurer l’intégration d’Azure AD à SAP NetWeaver, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="398e3-111">To configure Azure AD integration with SAP NetWeaver, you need the following items:</span></span>

- <span data-ttu-id="398e3-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="398e3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="398e3-113">Un abonnement SAP NetWeaver pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="398e3-113">An SAP NetWeaver single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="398e3-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="398e3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="398e3-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="398e3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="398e3-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="398e3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="398e3-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="398e3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="398e3-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="398e3-118">Scenario description</span></span>
<span data-ttu-id="398e3-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="398e3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="398e3-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="398e3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="398e3-121">Ajout de SAP NetWeaver à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="398e3-121">Adding SAP NetWeaver from the gallery</span></span>
2. <span data-ttu-id="398e3-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="398e3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-netweaver-from-the-gallery"></a><span data-ttu-id="398e3-123">Ajout de SAP NetWeaver à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="398e3-123">Adding SAP NetWeaver from the gallery</span></span>
<span data-ttu-id="398e3-124">Pour configurer l’intégration de SAP NetWeaver à Azure AD, vous devez ajouter SAP NetWeaver depuis la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="398e3-124">To configure the integration of SAP NetWeaver into Azure AD, you need to add SAP NetWeaver from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="398e3-125">**Pour ajouter SAP NetWeaver à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="398e3-125">**To add SAP NetWeaver from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="398e3-126">Dans le volet de navigation gauche du **[Portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="398e3-126">In the **[Azure Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="398e3-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="398e3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="398e3-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="398e3-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="398e3-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="398e3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="398e3-133">Dans la zone de recherche, tapez **SAP NetWeaver**.</span><span class="sxs-lookup"><span data-stu-id="398e3-133">In the search box, type **SAP NetWeaver**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_search.png)

5. <span data-ttu-id="398e3-135">Dans le panneau de résultats, sélectionnez **SAP NetWeaver**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="398e3-135">In the results panel, select **SAP NetWeaver**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="398e3-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="398e3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="398e3-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec SAP NetWeaver à l’aide d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="398e3-138">In this section, you configure and test Azure AD single sign-on with SAP NetWeaver based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="398e3-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur SAP NetWeaver équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="398e3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SAP NetWeaver is to a user in Azure AD.</span></span> <span data-ttu-id="398e3-140">En d’autres termes, une relation entre un utilisateur Azure AD et l’utilisateur SAP NetWeaver associé doit être établie.</span><span class="sxs-lookup"><span data-stu-id="398e3-140">In other words, a link relationship between an Azure AD user and the related user in SAP NetWeaver needs to be established.</span></span>

<span data-ttu-id="398e3-141">Pour ce faire, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** dans SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="398e3-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SAP NetWeaver.</span></span>

<span data-ttu-id="398e3-142">Pour configurer et tester l’authentification unique Azure AD avec SAP NetWeaver, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="398e3-142">To configure and test Azure AD single sign-on with SAP NetWeaver, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="398e3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="398e3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="398e3-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="398e3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="398e3-145">**[Création d’un utilisateur de test SAP NetWeaver](#creating-an-sap-netweaver-test-user)** pour avoir un équivalent de Britta Simon dans SAP NetWeaver lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="398e3-145">**[Creating an SAP NetWeaver test user](#creating-an-sap-netweaver-test-user)** - to have a counterpart of Britta Simon in SAP NetWeaver that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="398e3-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="398e3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="398e3-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="398e3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="398e3-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="398e3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="398e3-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="398e3-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAP NetWeaver application.</span></span>

<span data-ttu-id="398e3-150">**Pour configurer l’authentification unique Azure AD avec SAP NetWeaver, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="398e3-150">**To configure Azure AD single sign-on with SAP NetWeaver, perform the following steps:**</span></span>

1. <span data-ttu-id="398e3-151">Dans le portail Azure, sur la page d’intégration de l’application **SAP NetWeaver**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="398e3-151">In the Azure portal, on the **SAP NetWeaver** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="398e3-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="398e3-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_samlbase.png)

3. <span data-ttu-id="398e3-155">Dans la section **SAP NetWeaver Domain and URLs** (Domaine et URL SAP NetWeaver), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="398e3-155">On the **SAP NetWeaver Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_url.png)

    <span data-ttu-id="398e3-157">a.</span><span class="sxs-lookup"><span data-stu-id="398e3-157">a.</span></span> <span data-ttu-id="398e3-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<your company instance of SAP NetWeaver>`</span><span class="sxs-lookup"><span data-stu-id="398e3-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<your company instance of SAP NetWeaver>`</span></span>

    <span data-ttu-id="398e3-159">b.</span><span class="sxs-lookup"><span data-stu-id="398e3-159">b.</span></span> <span data-ttu-id="398e3-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<your company instance of SAP NetWeaver>`</span><span class="sxs-lookup"><span data-stu-id="398e3-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<your company instance of SAP NetWeaver>`</span></span>

    <span data-ttu-id="398e3-161">c.</span><span class="sxs-lookup"><span data-stu-id="398e3-161">c.</span></span> <span data-ttu-id="398e3-162">Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://<your company instance of SAP NetWeaver>/sap/saml2/sp/acs/100`</span><span class="sxs-lookup"><span data-stu-id="398e3-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<your company instance of SAP NetWeaver>/sap/saml2/sp/acs/100`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="398e3-163">Il ne s’agit pas des valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="398e3-163">These values are not the real.</span></span> <span data-ttu-id="398e3-164">Mettez à jour ces valeurs avec l’identificateur et l’URL de réponse réels et l’URL de connexion.</span><span class="sxs-lookup"><span data-stu-id="398e3-164">Update these values with the actual Identifier and Reply URL and Sign-On URL.</span></span> <span data-ttu-id="398e3-165">Nous vous suggérons d’utiliser ici la valeur de chaîne unique dans l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="398e3-165">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="398e3-166">Pour obtenir ces valeurs, contactez [l’équipe de support technique SAP NetWeaver](https://www.sap.com/support.html).</span><span class="sxs-lookup"><span data-stu-id="398e3-166">Contact [SAP NetWeaver Client support team](https://www.sap.com/support.html) to get these values.</span></span> 

4. <span data-ttu-id="398e3-167">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier XML sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="398e3-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_certificate.png) 

5. <span data-ttu-id="398e3-169">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="398e3-169">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="398e3-171">Dans la section **SAP NetWeaver Configuration** (Configuration de SAP NetWeaver), cliquez sur **Configure SAP NetWeaver** (Configurer SAP NetWeaver) pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="398e3-171">On the **SAP NetWeaver Configuration** section, click **Configure SAP NetWeaver** to open **Configure sign-on** window.</span></span> <span data-ttu-id="398e3-172">Copiez **l’ID d’entité SAML** à partir de la **section Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="398e3-172">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_configure.png) 

7. <span data-ttu-id="398e3-174">Pour configurer l’authentification unique côté **SAP NetWeaver**, vous devez envoyer le fichier **XML de métadonnées** téléchargé et **l’ID d’entité SAML** à [l’équipe de support SAP NetWeaver](https://www.sap.com/support.html).</span><span class="sxs-lookup"><span data-stu-id="398e3-174">To configure single sign-on on **SAP NetWeaver** side, you need to send the downloaded **Metadata XML** and **SAML Entity ID** to [SAP NetWeaver support](https://www.sap.com/support.html).</span></span> 

> [!TIP]
> <span data-ttu-id="398e3-175">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="398e3-175">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="398e3-176">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="398e3-176">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="398e3-177">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="398e3-177">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="398e3-178">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="398e3-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="398e3-179">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="398e3-179">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="398e3-181">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="398e3-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="398e3-182">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="398e3-182">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="398e3-184">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="398e3-184">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="398e3-186">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="398e3-186">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="398e3-188">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="398e3-188">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-netweaver-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="398e3-190">a.</span><span class="sxs-lookup"><span data-stu-id="398e3-190">a.</span></span> <span data-ttu-id="398e3-191">Dans la zone de texte **Name**, entrez **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="398e3-191">In the **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="398e3-192">b.</span><span class="sxs-lookup"><span data-stu-id="398e3-192">b.</span></span> <span data-ttu-id="398e3-193">Dans la zone de texte **Nom d’utilisateur** , tapez l’**adresse de messagerie** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="398e3-193">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="398e3-194">c.</span><span class="sxs-lookup"><span data-stu-id="398e3-194">c.</span></span> <span data-ttu-id="398e3-195">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="398e3-195">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="398e3-196">d.</span><span class="sxs-lookup"><span data-stu-id="398e3-196">d.</span></span> <span data-ttu-id="398e3-197">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="398e3-197">Click **Create**.</span></span>
 
### <a name="creating-an-sap-netweaver-test-user"></a><span data-ttu-id="398e3-198">Création d’un utilisateur de test de SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="398e3-198">Creating an SAP NetWeaver test user</span></span>

<span data-ttu-id="398e3-199">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="398e3-199">In this section, you create a user called Britta Simon in SAP NetWeaver.</span></span> <span data-ttu-id="398e3-200">Travaillez avec votre [support technique SAP NetWeaver](https://www.sap.com/support.html) pour ajouter les utilisateurs à la plateforme SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="398e3-200">Work with your [SAP NetWeaver support](https://www.sap.com/support.html) to add the users in the SAP NetWeaver platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="398e3-201">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="398e3-201">Assigning the Azure AD test user</span></span>

<span data-ttu-id="398e3-202">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="398e3-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAP NetWeaver.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="398e3-204">**Pour affecter Britta Simon à SAP NetWeaver, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="398e3-204">**To assign Britta Simon to SAP NetWeaver, perform the following steps:**</span></span>

1. <span data-ttu-id="398e3-205">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="398e3-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="398e3-207">Dans la liste des applications, sélectionnez **SAP NetWeaver**.</span><span class="sxs-lookup"><span data-stu-id="398e3-207">In the applications list, select **SAP NetWeaver**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sap-netweaver-tutorial/tutorial_sapnetweaver_app.png) 

3. <span data-ttu-id="398e3-209">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="398e3-209">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="398e3-211">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="398e3-211">Click **Add** button.</span></span> <span data-ttu-id="398e3-212">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="398e3-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="398e3-214">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="398e3-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="398e3-215">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="398e3-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="398e3-216">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="398e3-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="398e3-217">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="398e3-217">Testing single sign-on</span></span>

<span data-ttu-id="398e3-218">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="398e3-218">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="398e3-219">Lorsque vous cliquez sur la mosaïque SAP NetWeaver dans le volet d’accès, vous devez être connecté automatiquement à votre application SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="398e3-219">When you click the SAP NetWeaver tile in the Access Panel, you should get automatically signed-on to your SAP NetWeaver application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="398e3-220">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="398e3-220">Additional resources</span></span>

* [<span data-ttu-id="398e3-221">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="398e3-221">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="398e3-222">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="398e3-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-netweaver-tutorial/tutorial_general_203.png

