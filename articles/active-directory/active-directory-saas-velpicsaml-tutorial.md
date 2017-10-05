---
title: "Didacticiel : Intégration d’Azure Active Directory à Velpic SAML | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Velpic SAML."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 5325f3cca00167e6b7b687509ce43435447ad2f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-velpic-saml"></a><span data-ttu-id="f9fe4-103">Didacticiel : Intégration d’Azure Active Directory à Velpic SAML</span><span class="sxs-lookup"><span data-stu-id="f9fe4-103">Tutorial: Azure Active Directory integration with Velpic SAML</span></span>

<span data-ttu-id="f9fe4-104">Dans ce didacticiel, vous allez apprendre à intégrer Velpic SAML à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f9fe4-104">In this tutorial, you learn how to integrate Velpic SAML with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f9fe4-105">L’intégration de Velpic SAML à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="f9fe4-105">Integrating Velpic SAML with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f9fe4-106">Dans Azure AD, vous pouvez contrôler qui a accès à Velpic SAML</span><span class="sxs-lookup"><span data-stu-id="f9fe4-106">You can control in Azure AD who has access to Velpic SAML</span></span>
- <span data-ttu-id="f9fe4-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Velpic SAML (via l’authentification unique) avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="f9fe4-107">You can enable your users to automatically get signed-on to Velpic SAML (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f9fe4-108">Vous pouvez gérer vos comptes de manière centralisée dans le portail de gestion Azure.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="f9fe4-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f9fe4-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f9fe4-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f9fe4-110">Prerequisites</span></span>

<span data-ttu-id="f9fe4-111">Pour configurer l’intégration d’Azure AD à Velpic SAML, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f9fe4-111">To configure Azure AD integration with Velpic SAML, you need the following items:</span></span>

- <span data-ttu-id="f9fe4-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="f9fe4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f9fe4-113">Un abonnement Velpic SAML pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="f9fe4-113">A Velpic SAML single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f9fe4-114">Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f9fe4-115">Vous devez en outre suivre les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="f9fe4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f9fe4-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="f9fe4-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f9fe4-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f9fe4-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="f9fe4-118">Scenario description</span></span>
<span data-ttu-id="f9fe4-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f9fe4-120">Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="f9fe4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f9fe4-121">Ajout de Velpic SAML à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="f9fe4-121">Adding Velpic SAML from the gallery</span></span>
2. <span data-ttu-id="f9fe4-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f9fe4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-velpic-saml-from-the-gallery"></a><span data-ttu-id="f9fe4-123">Ajout de Velpic SAML à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="f9fe4-123">Adding Velpic SAML from the gallery</span></span>
<span data-ttu-id="f9fe4-124">Pour configurer l’intégration de Velpic SAML à Azure AD, vous devez ajouter Velpic SAML à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-124">To configure the integration of Velpic SAML into Azure AD, you need to add Velpic SAML from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f9fe4-125">**Pour ajouter Velpic SAML à partir de la galerie, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f9fe4-125">**To add Velpic SAML from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f9fe4-126">Dans le panneau de navigation gauche du **[Portail de gestion Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f9fe4-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f9fe4-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="f9fe4-131">Cliquez sur le bouton **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="f9fe4-133">Dans la zone de recherche, tapez **Velpic SAML**.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-133">In the search box, type **Velpic SAML**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_search.png)

5. <span data-ttu-id="f9fe4-135">Dans le volet des résultats, sélectionnez **Velpic SAML**, puis cliquez sur **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-135">In the results panel, select **Velpic SAML**, and then click **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f9fe4-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f9fe4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f9fe4-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Velpic SAML avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="f9fe4-138">In this section, you configure and test Azure AD single sign-on with Velpic SAML based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f9fe4-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Velpic SAML équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Velpic SAML is to a user in Azure AD.</span></span> <span data-ttu-id="f9fe4-140">En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur associé dans Velpic SAML doit être établie.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-140">In other words, a link relationship between an Azure AD user and the related user in Velpic SAML needs to be established.</span></span>

<span data-ttu-id="f9fe4-141">Pour ce faire, affectez la valeur du champ **nom d’utilisateur** d’Azure AD comme valeur du champ **Username** (Nom d’utilisateur) dans Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Velpic SAML.</span></span>

<span data-ttu-id="f9fe4-142">Pour configurer et tester l’authentification unique Azure AD avec Velpic SAML, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="f9fe4-142">To configure and test Azure AD single sign-on with Velpic SAML, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f9fe4-143">**[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f9fe4-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f9fe4-145">**[Création d’un utilisateur de test Velpic SAML](#creating-a-velpic-saml-test-user)** : pour avoir un équivalent de Britta Simon dans Velpic SAML lié à la représentation Azure AD associée.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-145">**[Creating a Velpic SAML test user](#creating-a-velpic-saml-test-user)** - to have a counterpart of Britta Simon in Velpic SAML that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="f9fe4-146">**[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d'utiliser l'authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f9fe4-147">**[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f9fe4-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f9fe4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f9fe4-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail de gestion Azure et configurer l’authentification unique dans votre application Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Velpic SAML application.</span></span>

<span data-ttu-id="f9fe4-150">**Pour configurer l’authentification unique Azure AD avec Velpic SAML, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f9fe4-150">**To configure Azure AD single sign-on with Velpic SAML, perform the following steps:**</span></span>

1. <span data-ttu-id="f9fe4-151">Dans le portail de gestion Azure, sur la page d’intégration de l’application **Velpic SAML**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-151">In the Azure Management portal, on the **Velpic SAML** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="f9fe4-153">Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_samlbase.png)

3. <span data-ttu-id="f9fe4-155">Entrez les détails dans la section **Domaine et URL Velpic SAML** -</span><span class="sxs-lookup"><span data-stu-id="f9fe4-155">Enter the details in the **Velpic SAML Domain and URLs** section-</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_url.png)

    <span data-ttu-id="f9fe4-157">a.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-157">a.</span></span> <span data-ttu-id="f9fe4-158">Dans la zone de texte **URL de connexion**, tapez la valeur suivante : `https://<sub-domain>.velpicsaml.net`</span><span class="sxs-lookup"><span data-stu-id="f9fe4-158">In the **Sign-on URL** textbox, type the value as: `https://<sub-domain>.velpicsaml.net`</span></span>

    <span data-ttu-id="f9fe4-159">b.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-159">b.</span></span> <span data-ttu-id="f9fe4-160">Dans la zone de texte **Identificateur**, collez la valeur **URL d'authentification unique** `https://auth.velpic.com/saml/v2/<entity-id>/login`</span><span class="sxs-lookup"><span data-stu-id="f9fe4-160">In the **Identifier** textbox, paste the **‘Single sign on URL’** value `https://auth.velpic.com/saml/v2/<entity-id>/login`</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="f9fe4-161">Notez que l’URL d’authentification unique sera fournie par l’équipe Velpic SAML et la valeur Identificateur sera disponible lorsque vous configurez le plug-in SSO du côté Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-161">Please note that the Sign on URL will be provided by the Velpic SAML team and Identifier value will be available when you configure the SSO Plugin on Velpic SAML side.</span></span> <span data-ttu-id="f9fe4-162">Vous devez copier cette valeur à partir de la page d’application Velpic SAML et la coller ici.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-162">You need to copy that value from Velpic SAML application  page and paste it here.</span></span>

4. <span data-ttu-id="f9fe4-163">Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier XML sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-163">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_certificate.png) 

5. <span data-ttu-id="f9fe4-165">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="f9fe4-165">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f9fe4-167">Dans la section Configuration de Velpic SAML, cliquez sur Configurer Velpic SAML pour ouvrir la fenêtre Configurer l’authentification.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-167">On the Velpic SAML Configuration section, click Configure Velpic SAML to open Configure sign-on window.</span></span> <span data-ttu-id="f9fe4-168">Copiez l’ID d’entité SAML à partir de la section Référence rapide.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-168">Copy the SAML Entity ID from the Quick Reference section.</span></span>

7. <span data-ttu-id="f9fe4-169">Dans une autre fenêtre de navigateur web, connectez-vous au site de votre entreprise Velpic SAML en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-169">In a different web browser window, log into your Velpic SAML company site as an administrator.</span></span>

8. <span data-ttu-id="f9fe4-170">Cliquez sur l’onglet **Gérer** et accédez à la section **Intégration** dans laquelle vous devez cliquer sur **Plug-ins** afin de créer le nouveau plug-in pour la connexion.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-170">Click on **Manage** tab and go to **Integration** section where you need to click on **Plugins** button to create new plugin for Sign-In.</span></span>

    ![Plug-in](./media/active-directory-saas-velpicsaml-tutorial/velpic_1.png)

9. <span data-ttu-id="f9fe4-172">Cliquez sur le bouton **Ajouter un plug-in**.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-172">Click on the **‘Add plugin’** button.</span></span>
    
    ![Plug-in](./media/active-directory-saas-velpicsaml-tutorial/velpic_2.png)

10. <span data-ttu-id="f9fe4-174">Cliquez sur la mosaïque **SAML** dans la page Ajouter un plug-in.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-174">Click on the **SAML** tile in the Add Plugin page.</span></span>
    
    ![Plug-in](./media/active-directory-saas-velpicsaml-tutorial/velpic_3.png)

11. <span data-ttu-id="f9fe4-176">Entrez le nom du nouveau plug-in SAML puis cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-176">Enter the name of the new SAML plugin and click the **‘Add’** button.</span></span>

    ![Plug-in](./media/active-directory-saas-velpicsaml-tutorial/velpic_4.png)

12. <span data-ttu-id="f9fe4-178">Entrez les informations comme suit :</span><span class="sxs-lookup"><span data-stu-id="f9fe4-178">Enter the details as follows:</span></span>

    ![Plug-in](./media/active-directory-saas-velpicsaml-tutorial/velpic_5.png)

    <span data-ttu-id="f9fe4-180">a.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-180">a.</span></span> <span data-ttu-id="f9fe4-181">Dans la zone de texte **Nom**, saisissez le nom du plug-in SAML.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-181">In the **Name** textbox, type the name of SAML plugin.</span></span>

    <span data-ttu-id="f9fe4-182">b.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-182">b.</span></span> <span data-ttu-id="f9fe4-183">Dans la zone de texte **URL de l’émetteur**, collez l**’ID d’entité SAML** que vous avez copié à partir de la fenêtre **Configurer l’authentification** du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-183">In the **Issuer URL** textbox, paste the **SAML Entity ID** you copied from the **Configure sign-on** window of the Azure portal.</span></span>

    <span data-ttu-id="f9fe4-184">c.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-184">c.</span></span> <span data-ttu-id="f9fe4-185">Dans la section **Configuration des métadonnées du fournisseur**, téléchargez le fichier XML de métadonnées que vous avez téléchargé à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-185">In the **Provider Metadata Config** upload the Metadata XML file which you downloaded from Azure portal.</span></span>

    <span data-ttu-id="f9fe4-186">d.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-186">d.</span></span> <span data-ttu-id="f9fe4-187">Vous pouvez également choisir d’activer l’approvisionnement immédiat SAML en cochant la case **Créer automatiquement les nouveaux utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-187">You can also choose to enable SAML just in time provisioning by enabling the **‘Auto create new users’** checkbox.</span></span> <span data-ttu-id="f9fe4-188">Si un utilisateur n’existe pas dans Velpic et que cet indicateur n’est pas activé, la connexion à partir d’Azure échouera.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-188">If a user doesn’t exist in Velpic and this flag is not enabled, the login from Azure will fail.</span></span> <span data-ttu-id="f9fe4-189">Si l’indicateur est activé, l’utilisateur sera automatiquement approvisionné dans Velpic au moment de la connexion.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-189">If the flag is enabled the user will automatically be provisioned into Velpic at the time of login.</span></span> 

    <span data-ttu-id="f9fe4-190">e.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-190">e.</span></span> <span data-ttu-id="f9fe4-191">Copiez l**’URL d’authentification unique** à partir de la zone de texte et collez-la dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-191">Copy the **Single sign on URL** from the text box and paste it in the Azure portal.</span></span>
    
    <span data-ttu-id="f9fe4-192">f.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-192">f.</span></span> <span data-ttu-id="f9fe4-193">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-193">Click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f9fe4-194">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="f9fe4-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="f9fe4-195">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le Portail de gestion Azure.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-195">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="f9fe4-197">**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f9fe4-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f9fe4-198">Dans le panneau de navigation gauche du **Portail de gestion Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-198">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f9fe4-200">Accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs** pour afficher la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-200">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f9fe4-202">En haut de la boîte de dialogue, cliquez sur **Ajouter** pour ouvrir la boîte de dialogue **Utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-202">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f9fe4-204">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f9fe4-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f9fe4-206">a.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-206">a.</span></span> <span data-ttu-id="f9fe4-207">Dans la zone de texte **Nom**, entrez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f9fe4-208">b.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-208">b.</span></span> <span data-ttu-id="f9fe4-209">Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f9fe4-210">c.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-210">c.</span></span> <span data-ttu-id="f9fe4-211">Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f9fe4-212">d.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-212">d.</span></span> <span data-ttu-id="f9fe4-213">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-213">Click **Create**.</span></span>
 
### <a name="creating-a-velpic-saml-test-user"></a><span data-ttu-id="f9fe4-214">Création d’un utilisateur de test Velpic SAML</span><span class="sxs-lookup"><span data-stu-id="f9fe4-214">Creating a Velpic SAML test user</span></span>

<span data-ttu-id="f9fe4-215">Cette étape n’est généralement pas nécessaire car l’application prend en charge l’approvisionnement immédiat de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-215">This step is usually not required as the application supports just in time user provisioning.</span></span> <span data-ttu-id="f9fe4-216">Si l’approvisionnement automatique de l’utilisateur n’est pas activé, la création manuelle de l’utilisateur peut être effectuée comme décrit ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-216">If the automatic user provisioning is not enabled then manual user creation can be done as described below.</span></span>

<span data-ttu-id="f9fe4-217">Connectez-vous au site de votre entreprise Velpic SAML en tant qu’administrateur et effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="f9fe4-217">Log into your Velpic SAML company site as an administrator and perform following steps:</span></span>
    
1. <span data-ttu-id="f9fe4-218">Cliquez sur l’onglet Gérer et accédez à la section Utilisateurs, puis cliquez sur le bouton Nouveau pour ajouter des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-218">Click on Manage tab and go to Users section, then click on New button to add users.</span></span>

    ![ajouter un utilisateur](./media/active-directory-saas-velpicsaml-tutorial/velpic_7.png)

2. <span data-ttu-id="f9fe4-220">Dans la boîte de dialogue **Create New User**, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-220">On the **“Create New User”** dialog page, perform the following steps.</span></span>

    ![user](./media/active-directory-saas-velpicsaml-tutorial/velpic_8.png)
    
    <span data-ttu-id="f9fe4-222">a.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-222">a.</span></span> <span data-ttu-id="f9fe4-223">Dans la zone de texte **First Name**, tapez le prénom de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-223">In the **First Name** textbox, type the first name of Britta Simon.</span></span>

    <span data-ttu-id="f9fe4-224">b.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-224">b.</span></span> <span data-ttu-id="f9fe4-225">Dans la zone de texte **Last Name**, tapez le nom de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-225">In the **Last Name** textbox, type the last name of Britta Simon.</span></span>

    <span data-ttu-id="f9fe4-226">c.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-226">c.</span></span> <span data-ttu-id="f9fe4-227">Dans la zone de texte **User Name**, tapez le nom d’utilisateur de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-227">In the **User Name** textbox, type the user name of Britta Simon.</span></span>

    <span data-ttu-id="f9fe4-228">d.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-228">d.</span></span> <span data-ttu-id="f9fe4-229">Dans la zone de texte **E-mail** , tapez l’adresse de messagerie du compte de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-229">In the **Email** textbox, type the email address of Britta Simon account.</span></span>

    <span data-ttu-id="f9fe4-230">e.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-230">e.</span></span> <span data-ttu-id="f9fe4-231">Les autres informations sont facultatives et vous pouvez les renseigner si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-231">Rest of the information is optional, you can fill it if needed.</span></span>
    
    <span data-ttu-id="f9fe4-232">f.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-232">f.</span></span> <span data-ttu-id="f9fe4-233">Cliquez sur **ENREGISTRER**.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-233">Click **SAVE**.</span></span>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f9fe4-234">Affectation de l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="f9fe4-234">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f9fe4-235">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-235">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Velpic SAML.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="f9fe4-237">**Pour affecter Britta Simon à Velpic SAML, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f9fe4-237">**To assign Britta Simon to Velpic SAML, perform the following steps:**</span></span>

1. <span data-ttu-id="f9fe4-238">Dans le portail de gestion Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-238">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="f9fe4-240">Dans la liste des applications, sélectionnez **Velpic SAML**.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-240">In the applications list, select **Velpic SAML**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_app.png) 

3. <span data-ttu-id="f9fe4-242">Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-242">In the menu on the left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="f9fe4-244">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-244">Click **Add** button.</span></span> <span data-ttu-id="f9fe4-245">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="f9fe4-247">Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f9fe4-248">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f9fe4-249">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f9fe4-250">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="f9fe4-250">Testing single sign-on</span></span>

<span data-ttu-id="f9fe4-251">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-251">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

1. <span data-ttu-id="f9fe4-252">Lorsque vous cliquez sur la mosaïque Velpic SAML dans le volet d’accès, la page de connexion de l’application Velpic SAML devrait apparaître.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-252">When you click the Velpic SAML tile in the Access Panel, you should get login page of Velpic SAML application.</span></span> <span data-ttu-id="f9fe4-253">Vous devriez voir le bouton **Se connecter à Azure AD** sur la page de connexion.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-253">You should see the **‘Log In With Azure AD’** button on the sign in page.</span></span>

    ![Plug-in](./media/active-directory-saas-velpicsaml-tutorial/velpic_6.png)

2. <span data-ttu-id="f9fe4-255">Cliquez sur le bouton **Se connecter à Azure AD** pour vous connecter à Velpic à l’aide de votre compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f9fe4-255">Click on the **‘Log In With Azure AD’** button to log in to Velpic using your Azure AD account.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="f9fe4-256">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="f9fe4-256">Additional resources</span></span>

* [<span data-ttu-id="f9fe4-257">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f9fe4-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f9fe4-258">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="f9fe4-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_203.png

