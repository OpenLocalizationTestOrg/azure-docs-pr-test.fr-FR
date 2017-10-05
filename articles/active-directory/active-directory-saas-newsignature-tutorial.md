---
title: "Didacticiel : Intégration d’Azure Active Directory à Cloud Management Portal for Microsoft Azure | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Cloud Management Portal for Microsoft Azure."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4ea9f47c-25ca-42b0-a878-9e7aa6f34973
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: bae5f05a161b2730bf662bcb47f20ab3e1799951
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cloud-management-portal-for-microsoft-azure"></a><span data-ttu-id="fbe6e-103">Didacticiel : Intégration d’Azure Active Directory à Cloud Management Portal for Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="fbe6e-103">Tutorial: Azure Active Directory integration with Cloud Management Portal for Microsoft Azure</span></span>

<span data-ttu-id="fbe6e-104">Dans ce didacticiel, vous allez apprendre à intégrer Cloud Management Portal for Microsoft Azure à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fbe6e-104">In this tutorial, you learn how to integrate Cloud Management Portal for Microsoft Azure with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fbe6e-105">L’intégration du portail de gestion cloud de Microsoft Azure avec Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="fbe6e-105">Integrating Cloud Management Portal for Microsoft Azure with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="fbe6e-106">Vous pouvez contrôler dans Azure AD qui a accès à Cloud Management Portal for Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-106">You can control in Azure AD who has access to Cloud Management Portal for Microsoft Azure</span></span>
- <span data-ttu-id="fbe6e-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Cloud Management Portal for Microsoft Azure (par le biais de l’authentification unique) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-107">You can enable your users to automatically get signed-on to Cloud Management Portal for Microsoft Azure (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fbe6e-108">Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="fbe6e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="fbe6e-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fbe6e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fbe6e-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="fbe6e-110">Prerequisites</span></span>

<span data-ttu-id="fbe6e-111">Pour configurer l’intégration d’Azure AD à Cloud Management Portal for Microsoft Azure, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="fbe6e-111">To configure Azure AD integration with Cloud Management Portal for Microsoft Azure, you need the following items:</span></span>

- <span data-ttu-id="fbe6e-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbe6e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fbe6e-113">Un abonnement Cloud Management Portal for Microsoft Azure pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="fbe6e-113">A Cloud Management Portal for Microsoft Azure single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fbe6e-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fbe6e-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="fbe6e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fbe6e-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fbe6e-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fbe6e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fbe6e-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="fbe6e-118">Scenario description</span></span>
<span data-ttu-id="fbe6e-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fbe6e-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="fbe6e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fbe6e-121">Ajout de Cloud Management Portal for Microsoft Azure à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="fbe6e-121">Adding Cloud Management Portal for Microsoft Azure from the gallery</span></span>
2. <span data-ttu-id="fbe6e-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbe6e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cloud-management-portal-for-microsoft-azure-from-the-gallery"></a><span data-ttu-id="fbe6e-123">Ajout de Cloud Management Portal for Microsoft Azure à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="fbe6e-123">Adding Cloud Management Portal for Microsoft Azure from the gallery</span></span>
<span data-ttu-id="fbe6e-124">Pour configurer l’intégration de Cloud Management Portal for Microsoft Azure à Azure AD, vous devez ajouter Cloud Management Portal for Microsoft Azure à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-124">To configure the integration of Cloud Management Portal for Microsoft Azure into Azure AD, you need to add Cloud Management Portal for Microsoft Azure from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="fbe6e-125">**Pour ajouter Cloud Management Portal for Microsoft Azure à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="fbe6e-125">**To add Cloud Management Portal for Microsoft Azure from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="fbe6e-126">Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fbe6e-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="fbe6e-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="fbe6e-131">Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="fbe6e-133">Dans la zone de recherche, tapez **Cloud Management Portal for Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-133">In the search box, type **Cloud Management Portal for Microsoft Azure**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_search.png)

5. <span data-ttu-id="fbe6e-135">Dans le volet de résultats, sélectionnez **Cloud Management Portal for Microsoft Azure**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-135">In the results panel, select **Cloud Management Portal for Microsoft Azure**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fbe6e-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbe6e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fbe6e-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Cloud Management Portal for Microsoft Azure avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="fbe6e-138">In this section, you configure and test Azure AD single sign-on with Cloud Management Portal for Microsoft Azure based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="fbe6e-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Cloud Management Portal for Microsoft Azure équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Cloud Management Portal for Microsoft Azure is to a user in Azure AD.</span></span> <span data-ttu-id="fbe6e-140">En d’autres termes, un lien entre un utilisateur Azure AD et l’utilisateur Cloud Management Portal for Microsoft Azure associé doit être établi.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-140">In other words, a link relationship between an Azure AD user and the related user in Cloud Management Portal for Microsoft Azure needs to be established.</span></span>

<span data-ttu-id="fbe6e-141">Dans Cloud Management Portal for Microsoft Azure, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-141">In Cloud Management Portal for Microsoft Azure, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="fbe6e-142">Pour configurer et tester l’authentification unique Azure AD avec Cloud Management Portal for Microsoft Azure, vous avez besoin de suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="fbe6e-142">To configure and test Azure AD single sign-on with Cloud Management Portal for Microsoft Azure, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="fbe6e-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="fbe6e-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fbe6e-145">**[Création d’un utilisateur de test Cloud Management Portal for Microsoft Azure](#creating-a-cloud-management-portal-for-microsoft-azure-test-user)** pour avoir un équivalent de Britta Simon dans Cloud Management Portal for Microsoft Azure lié à la représentation Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-145">**[Creating a Cloud Management Portal for Microsoft Azure test user](#creating-a-cloud-management-portal-for-microsoft-azure-test-user)** - to have a counterpart of Britta Simon in Cloud Management Portal for Microsoft Azure that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="fbe6e-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fbe6e-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fbe6e-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbe6e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fbe6e-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Cloud Management Portal for Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cloud Management Portal for Microsoft Azure application.</span></span>

<span data-ttu-id="fbe6e-150">**Pour configurer l’authentification unique Azure AD avec Cloud Management Portal for Microsoft Azure, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="fbe6e-150">**To configure Azure AD single sign-on with Cloud Management Portal for Microsoft Azure, perform the following steps:**</span></span>

1. <span data-ttu-id="fbe6e-151">Dans le portail Azure, dans la page d’intégration de l’application **Cloud Management Portal for Microsoft Azure**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-151">In the Azure portal, on the **Cloud Management Portal for Microsoft Azure** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="fbe6e-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_samlbase.png)

3. <span data-ttu-id="fbe6e-155">Dans la section **Domaine et URL Cloud Management Portal for Microsoft Azure**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="fbe6e-155">On the **Cloud Management Portal for Microsoft Azure Domain and URLs** section, perform the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_url.png)

    <span data-ttu-id="fbe6e-157">a.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-157">a.</span></span> <span data-ttu-id="fbe6e-158">Dans la zone de texte **URL de connexion**, tapez une URL au format suivant :</span><span class="sxs-lookup"><span data-stu-id="fbe6e-158">In the **Sign-on URL** textbox, type a URL using the following patterns:</span></span> 
    
    | |
    |--|
    | `https://portal.newsignature.com/<instancename>` |   
    | `https://portal.igcm.com/<instancename>` |
    
    <span data-ttu-id="fbe6e-159">b.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-159">b.</span></span> <span data-ttu-id="fbe6e-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant :</span><span class="sxs-lookup"><span data-stu-id="fbe6e-160">In the **Identifier** textbox, type a URL using the following patterns:</span></span> 
    
    | |
    |--|
    | `https://<subdomain>.igcm.com` |
    | `https://<subdomain>.newsignature.com` |

    <span data-ttu-id="fbe6e-161">c.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-161">c.</span></span> <span data-ttu-id="fbe6e-162">Dans la zone de texte **URL de réponse** , tapez une URL en respectant les formats suivants :</span><span class="sxs-lookup"><span data-stu-id="fbe6e-162">In the **Reply URL** textbox, type a URL using the following patterns:</span></span> 
    
    | |
    |--|
    | `https://<subdomain>.igcm.com/<instancename>` |
    | `https://<subdomain>.newsignature.com` |
    | `https://<subdomain>.newsignature.com/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="fbe6e-163">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-163">These values are not real.</span></span> <span data-ttu-id="fbe6e-164">Mettez à jour ces valeurs avec l’URL de connexion, l’identificateur et l’URL de réponse réels.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-164">Update these values with the actual Sign-On URL, Identifier and Reply URL.</span></span> <span data-ttu-id="fbe6e-165">Pour obtenir ces valeurs, contactez [l’équipe du support client Cloud Management Portal for Microsoft Azure](mailto:jczernuszka@newsignature.com).</span><span class="sxs-lookup"><span data-stu-id="fbe6e-165">Contact [Cloud Management Portal for Microsoft Azure Client support team](mailto:jczernuszka@newsignature.com) to get these values.</span></span> 
 
4. <span data-ttu-id="fbe6e-166">Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-166">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_certificate.png) 

5. <span data-ttu-id="fbe6e-168">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="fbe6e-168">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-newsignature-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="fbe6e-170">Dans la section **Configuration de Cloud Management Portal for Microsoft Azure**, cliquez sur **Configurer Cloud Management Portal for Microsoft Azure** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-170">On the **Cloud Management Portal for Microsoft Azure Configuration** section, click **Configure Cloud Management Portal for Microsoft Azure** to open **Configure sign-on** window.</span></span> <span data-ttu-id="fbe6e-171">Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="fbe6e-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_configure.png) 

7. <span data-ttu-id="fbe6e-173">Pour configurer l’authentification unique côté **Cloud Management Portal for Microsoft Azure**, vous devez envoyer le **certificat** téléchargé, **l’URL de déconnexion**, **l’URL du service d’authentification unique SAML** et **l’ID d’entité SAML** à [l’équipe du support technique Cloud Management Portal for Microsoft Azure](mailto:jczernuszka@newsignature.com).</span><span class="sxs-lookup"><span data-stu-id="fbe6e-173">To configure single sign-on on **Cloud Management Portal for Microsoft Azure** side, you need to send the downloaded **Certificate**, **Sign-Out URL**, **SAML Single Sign-On Service URL** and **SAML Entity ID** to [Cloud Management Portal for Microsoft Azure support team](mailto:jczernuszka@newsignature.com).</span></span> <span data-ttu-id="fbe6e-174">Elle configure ce paramètre pour que la connexion SSO SAML soit définie correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-174">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="fbe6e-175">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-175">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="fbe6e-176">Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-176">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="fbe6e-177">Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fbe6e-177">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fbe6e-178">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbe6e-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="fbe6e-179">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-179">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="fbe6e-181">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="fbe6e-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="fbe6e-182">Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-182">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-newsignature-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fbe6e-184">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-184">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-newsignature-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fbe6e-186">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-186">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-newsignature-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fbe6e-188">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="fbe6e-188">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-newsignature-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fbe6e-190">a.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-190">a.</span></span> <span data-ttu-id="fbe6e-191">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-191">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fbe6e-192">b.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-192">b.</span></span> <span data-ttu-id="fbe6e-193">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-193">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fbe6e-194">c.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-194">c.</span></span> <span data-ttu-id="fbe6e-195">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-195">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="fbe6e-196">d.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-196">d.</span></span> <span data-ttu-id="fbe6e-197">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-197">Click **Create**.</span></span>
 
### <a name="creating-a-cloud-management-portal-for-microsoft-azure-test-user"></a><span data-ttu-id="fbe6e-198">Création d’un utilisateur de test Cloud Management Portal for Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="fbe6e-198">Creating a Cloud Management Portal for Microsoft Azure test user</span></span>

<span data-ttu-id="fbe6e-199">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans Cloud Management Portal for Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-199">The objective of this section is to create a user called Britta Simon in Cloud Management Portal for Microsoft Azure.</span></span> <span data-ttu-id="fbe6e-200">Collaborez avec [l’équipe du support technique Cloud Management Portal for Microsoft Azure](mailto:jczernuszka@newsignature.com) pour ajouter les utilisateurs au compte Cloud Management Portal for Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-200">Please work with [Cloud Management Portal for Microsoft Azure support team](mailto:jczernuszka@newsignature.com) to add the users in the Cloud Management Portal for Microsoft Azure account.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="fbe6e-201">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="fbe6e-201">Assigning the Azure AD test user</span></span>

<span data-ttu-id="fbe6e-202">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Cloud Management Portal for Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cloud Management Portal for Microsoft Azure.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="fbe6e-204">**Pour affecter Britta Simon à Cloud Management Portal for Microsoft Azure, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="fbe6e-204">**To assign Britta Simon to Cloud Management Portal for Microsoft Azure, perform the following steps:**</span></span>

1. <span data-ttu-id="fbe6e-205">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="fbe6e-207">Dans la liste des applications, sélectionnez **Cloud Management Portal for Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-207">In the applications list, select **Cloud Management Portal for Microsoft Azure**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-newsignature-tutorial/tutorial_newsignature_app.png) 

3. <span data-ttu-id="fbe6e-209">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-209">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="fbe6e-211">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-211">Click **Add** button.</span></span> <span data-ttu-id="fbe6e-212">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="fbe6e-214">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="fbe6e-215">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fbe6e-216">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fbe6e-217">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="fbe6e-217">Testing single sign-on</span></span>

<span data-ttu-id="fbe6e-218">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-218">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>
<span data-ttu-id="fbe6e-219">Quand vous cliquez sur la vignette Cloud Management Portal for Microsoft Azure dans le volet d’accès, vous devez être connecté automatiquement à votre application Cloud Management Portal for Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="fbe6e-219">When you click the Cloud Management Portal for Microsoft Azure tile in the Access Panel, you should get automatically signed-on to your Cloud Management Portal for Microsoft Azure application.</span></span>

<span data-ttu-id="fbe6e-220">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fbe6e-220">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fbe6e-221">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="fbe6e-221">Additional resources</span></span>

* [<span data-ttu-id="fbe6e-222">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fbe6e-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fbe6e-223">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="fbe6e-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-newsignature-tutorial/tutorial_general_203.png

