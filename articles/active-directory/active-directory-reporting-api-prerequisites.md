---
title: "Configuration requise pour accéder à l’API de création de rapports Azure AD. | Microsoft Docs"
description: "En savoir plus sur la configuration requise pour accéder à l’API de création de rapports Azure AD"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: ada19f69-665c-452a-8452-701029bf4252
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 6e409fc56b77f37dac7f37382e664c577666ad4d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="prerequisites-to-access-the-azure-ad-reporting-api"></a><span data-ttu-id="c56c6-104">Configuration requise pour accéder à l’API de création de rapports Azure AD</span><span class="sxs-lookup"><span data-stu-id="c56c6-104">Prerequisites to access the Azure AD reporting API</span></span>
<span data-ttu-id="c56c6-105">Les [API de création de rapports Azure AD](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) vous fournissent un accès par programme aux données via un ensemble d’API REST.</span><span class="sxs-lookup"><span data-stu-id="c56c6-105">The [Azure AD reporting APIs](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) provide you with programmatic access to the data through a set of REST-based APIs.</span></span> <span data-ttu-id="c56c6-106">Vous pouvez appeler ces API à partir de divers outils et langages de programmation.</span><span class="sxs-lookup"><span data-stu-id="c56c6-106">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="c56c6-107">L’API de création de rapports utilise [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) pour autoriser l’accès aux API web.</span><span class="sxs-lookup"><span data-stu-id="c56c6-107">The reporting API uses [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) to authorize access to the web APIs.</span></span> 

<span data-ttu-id="c56c6-108">Pour préparer votre accès à l’API de création de rapports, vous devez :</span><span class="sxs-lookup"><span data-stu-id="c56c6-108">To prepare your access to the reporting API, you must:</span></span>

1. <span data-ttu-id="c56c6-109">Créer une application dans votre client Azure AD</span><span class="sxs-lookup"><span data-stu-id="c56c6-109">Create an application in your Azure AD tenant</span></span> 
2. <span data-ttu-id="c56c6-110">Accorder les autorisations appropriées d’application pour accéder aux données Azure AD</span><span class="sxs-lookup"><span data-stu-id="c56c6-110">Grant the application appropriate permissions to access the Azure AD data</span></span>
3. <span data-ttu-id="c56c6-111">Collecter les paramètres de configuration de votre annuaire</span><span class="sxs-lookup"><span data-stu-id="c56c6-111">Gather configuration settings from your directory</span></span>

<span data-ttu-id="c56c6-112">Si vous avez des questions, des problèmes ou des commentaires, veuillez contacter [Aide à la création de rapports AAD](mailto:aadreportinghelp@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="c56c6-112">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>

## <a name="create-an-azure-ad-application"></a><span data-ttu-id="c56c6-113">Créer une application Azure AD</span><span class="sxs-lookup"><span data-stu-id="c56c6-113">Create an Azure AD application</span></span>
<span data-ttu-id="c56c6-114">Pour configurer votre annuaire et lui permettre d’accéder à l’API de création de rapports Azure AD, vous devez vous connecter au portail Azure Classic avec un compte d’administrateur d’abonnements Azure, également membre du rôle d’annuaire Administrateur général dans votre client Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c56c6-114">To configure your directory to access the Azure AD reporting API, you must sign in to the Azure classic portal with an Azure subscription administrator account that is also a member of the Global Administrator directory role in your Azure AD tenant.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c56c6-115">Les applications qui s’exécutent sous les informations d’identification pourvues de privilèges d’administrateur de ce type peuvent être très puissantes. Veillez donc à sécuriser les informations d’identification d’ID/du secret de l’application.</span><span class="sxs-lookup"><span data-stu-id="c56c6-115">Applications running under credentials with "admin" privileges like this can be very powerful, so please be sure to keep the application's ID/secret credentials secure.</span></span>
> 
> 

1. <span data-ttu-id="c56c6-116">Dans le volet de navigation gauche du [portail Azure Classic](https://manage.windowsazure.com), cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c56c6-116">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="c56c6-118">Dans la liste **active directory** , sélectionnez votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="c56c6-118">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="c56c6-119">Dans le menu supérieur, cliquez sur **Applications**.</span><span class="sxs-lookup"><span data-stu-id="c56c6-119">In the menu on the top, click **Applications**.</span></span>
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="c56c6-121">Dans la barre inférieure, cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="c56c6-121">On the bottom bar, click **Add**.</span></span>
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/03.png) 
5. <span data-ttu-id="c56c6-123">Sur la boîte de dialogue **Que voulez-vous faire ?**, cliquez sur **Ajouter une application développée par mon organisation**.</span><span class="sxs-lookup"><span data-stu-id="c56c6-123">On the **What do you want to do?** dialog, click **Add an application my organization is developing**.</span></span> 
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/04.png) 
6. <span data-ttu-id="c56c6-125">Dans la boîte de dialogue **Dites-nous en plus sur cet utilisateur** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c56c6-125">On the **Tell us about your application** dialog, perform the following steps:</span></span> 
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/05.png) 
   
    <span data-ttu-id="c56c6-127">a.</span><span class="sxs-lookup"><span data-stu-id="c56c6-127">a.</span></span> <span data-ttu-id="c56c6-128">Dans la zone de texte **Nom** , entrez un nom (par exemple : Application API Création de rapports).</span><span class="sxs-lookup"><span data-stu-id="c56c6-128">In the **Name** textbox, type a name (e.g.: Reporting API Application).</span></span>
   
    <span data-ttu-id="c56c6-129">b.</span><span class="sxs-lookup"><span data-stu-id="c56c6-129">b.</span></span> <span data-ttu-id="c56c6-130">Sélectionnez **Application Web et/ou API Web**.</span><span class="sxs-lookup"><span data-stu-id="c56c6-130">Select **Web application and/or web API**.</span></span>
   
    <span data-ttu-id="c56c6-131">c.</span><span class="sxs-lookup"><span data-stu-id="c56c6-131">c.</span></span> <span data-ttu-id="c56c6-132">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="c56c6-132">Click **Next**.</span></span>
7. <span data-ttu-id="c56c6-133">Dans la boîte de dialogue **Propriétés de l’application** , effectuez les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="c56c6-133">On the **App properties** dialog, perform the following steps:</span></span> 
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/06.png) 
   
    <span data-ttu-id="c56c6-135">a.</span><span class="sxs-lookup"><span data-stu-id="c56c6-135">a.</span></span> <span data-ttu-id="c56c6-136">Dans la zone de texte **URL d’authentification**, tapez `https://localhost`.</span><span class="sxs-lookup"><span data-stu-id="c56c6-136">In the **Sign-on URL** textbox, type `https://localhost`.</span></span>
   
    <span data-ttu-id="c56c6-137">b.</span><span class="sxs-lookup"><span data-stu-id="c56c6-137">b.</span></span> <span data-ttu-id="c56c6-138">Dans la zone de texte **URL ID d’application**, tapez ```https://localhost/ReportingApiApp```.</span><span class="sxs-lookup"><span data-stu-id="c56c6-138">In the **App ID URI** textbox, type ```https://localhost/ReportingApiApp```.</span></span>
   
    <span data-ttu-id="c56c6-139">c.</span><span class="sxs-lookup"><span data-stu-id="c56c6-139">c.</span></span> <span data-ttu-id="c56c6-140">Cliquez sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="c56c6-140">Click **Complete**.</span></span>

## <a name="grant-your-application-permission-to-use-the-api"></a><span data-ttu-id="c56c6-141">Autorisation d'utilisation de l'API pour votre application</span><span class="sxs-lookup"><span data-stu-id="c56c6-141">Grant your application permission to use the API</span></span>
1. <span data-ttu-id="c56c6-142">Dans le volet de navigation gauche du [portail Azure Classic](https://manage.windowsazure.com/), cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c56c6-142">In the [Azure classic portal](https://manage.windowsazure.com/), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="c56c6-144">Dans la liste **active directory** , sélectionnez votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="c56c6-144">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="c56c6-145">Dans le menu supérieur, cliquez sur **Applications**.</span><span class="sxs-lookup"><span data-stu-id="c56c6-145">In the menu on the top, click **Applications**.</span></span>
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/02.png)
4. <span data-ttu-id="c56c6-147">Dans la liste des applications, sélectionnez l’application nouvellement créée.</span><span class="sxs-lookup"><span data-stu-id="c56c6-147">In the applications list, select your newly created application.</span></span>
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="c56c6-149">Dans le menu situé en haut, cliquez sur **Configurer**.</span><span class="sxs-lookup"><span data-stu-id="c56c6-149">In the menu on the top, click **Configure**.</span></span>
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="c56c6-151">Dans la section **Autorisations pour d’autres applications**, pour la ressource **Azure Active Directory**, cliquez sur la liste déroulante **Autorisations d’application**, puis sélectionnez **Lire les données du répertoire**.</span><span class="sxs-lookup"><span data-stu-id="c56c6-151">In the **Permissions to other applications** section, for the **Azure Active Directory** resource, click the **Application Permissions** drop-down list, and then select **Read directory data**.</span></span>
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/09.png)
7. <span data-ttu-id="c56c6-153">Dans la barre inférieure, cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="c56c6-153">On the bottom bar, click **Save**.</span></span>
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/10.png)

## <a name="gather-configuration-settings-from-your-directory"></a><span data-ttu-id="c56c6-155">Collecter les paramètres de configuration de votre annuaire</span><span class="sxs-lookup"><span data-stu-id="c56c6-155">Gather configuration settings from your directory</span></span>
<span data-ttu-id="c56c6-156">Cette section vous montre comment obtenir les paramètres suivants à partir de votre annuaire :</span><span class="sxs-lookup"><span data-stu-id="c56c6-156">This section shows you how to get the following settings from your directory:</span></span>

* <span data-ttu-id="c56c6-157">Nom de domaine</span><span class="sxs-lookup"><span data-stu-id="c56c6-157">Domain name</span></span>
* <span data-ttu-id="c56c6-158">ID client</span><span class="sxs-lookup"><span data-stu-id="c56c6-158">Client ID</span></span>
* <span data-ttu-id="c56c6-159">Clé secrète client</span><span class="sxs-lookup"><span data-stu-id="c56c6-159">Client secret</span></span>

<span data-ttu-id="c56c6-160">Ces valeurs sont nécessaires lors de la configuration des appels à l’API de création de rapports.</span><span class="sxs-lookup"><span data-stu-id="c56c6-160">You need these values when configuring calls to the reporting API.</span></span> 

### <a name="get-your-domain-name"></a><span data-ttu-id="c56c6-161">Obtenir votre nom de domaine</span><span class="sxs-lookup"><span data-stu-id="c56c6-161">Get your domain name</span></span>
1. <span data-ttu-id="c56c6-162">Dans le volet de navigation gauche du [portail Azure Classic](https://manage.windowsazure.com), cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c56c6-162">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="c56c6-164">Dans la liste **active directory** , sélectionnez votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="c56c6-164">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="c56c6-165">Dans le menu situé en haut de l’écran, cliquez sur **Domaines**.</span><span class="sxs-lookup"><span data-stu-id="c56c6-165">In the menu on the top, click **Domains**.</span></span>
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/11.png) 
4. <span data-ttu-id="c56c6-167">Dans la colonne **Nom de domaine** , copiez le nom de votre domaine.</span><span class="sxs-lookup"><span data-stu-id="c56c6-167">In the **Domain Name** column, copy your domain name.</span></span>
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/12.png) 

### <a name="get-the-applications-client-id"></a><span data-ttu-id="c56c6-169">Obtenir l’ID client de l’application</span><span class="sxs-lookup"><span data-stu-id="c56c6-169">Get the application's client ID</span></span>
1. <span data-ttu-id="c56c6-170">Dans le volet de navigation gauche du [portail Azure Classic](https://manage.windowsazure.com), cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c56c6-170">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="c56c6-172">Dans la liste **active directory** , sélectionnez votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="c56c6-172">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="c56c6-173">Dans le menu supérieur, cliquez sur **Applications**.</span><span class="sxs-lookup"><span data-stu-id="c56c6-173">In the menu on the top, click **Applications**.</span></span>
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="c56c6-175">Dans la liste des applications, sélectionnez l’application nouvellement créée.</span><span class="sxs-lookup"><span data-stu-id="c56c6-175">In the applications list, select your newly created application.</span></span>
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="c56c6-177">Dans le menu situé en haut, cliquez sur **Configurer**.</span><span class="sxs-lookup"><span data-stu-id="c56c6-177">In the menu on the top, click **Configure**.</span></span>
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="c56c6-179">Copiez votre **ID Client**.</span><span class="sxs-lookup"><span data-stu-id="c56c6-179">Copy your **Client ID**.</span></span>
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/13.png)

### <a name="get-the-applications-client-secret"></a><span data-ttu-id="c56c6-181">Obtenir la clé secrète client de l’application</span><span class="sxs-lookup"><span data-stu-id="c56c6-181">Get the application's client secret</span></span>
<span data-ttu-id="c56c6-182">Pour obtenir la clé secrète client de l’application, vous devez créer une nouvelle clé et enregistrer sa valeur lors de l’enregistrement de la nouvelle clé car il est impossible de récupérer cette valeur ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="c56c6-182">To get your application's client secret, you need to create a new key and save its value upon saving the new key because it is not possible to retrieve this value later anymore.</span></span>

1. <span data-ttu-id="c56c6-183">Dans le volet de navigation gauche du [portail Azure Classic](https://manage.windowsazure.com), cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c56c6-183">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="c56c6-185">Dans la liste **active directory** , sélectionnez votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="c56c6-185">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="c56c6-186">Dans le menu supérieur, cliquez sur **Applications**.</span><span class="sxs-lookup"><span data-stu-id="c56c6-186">In the menu on the top, click **Applications**.</span></span>
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="c56c6-188">Dans la liste des applications, sélectionnez l’application nouvellement créée.</span><span class="sxs-lookup"><span data-stu-id="c56c6-188">In the applications list, select your newly created application.</span></span>
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="c56c6-190">Dans le menu situé en haut, cliquez sur **Configurer**.</span><span class="sxs-lookup"><span data-stu-id="c56c6-190">In the menu on the top, click **Configure**.</span></span>
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="c56c6-192">Dans la section **Clés** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="c56c6-192">In the **Keys** section, perform the following steps:</span></span> 
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/14.png)
   
    <span data-ttu-id="c56c6-194">a.</span><span class="sxs-lookup"><span data-stu-id="c56c6-194">a.</span></span> <span data-ttu-id="c56c6-195">Dans la liste de durée, sélectionnez une durée</span><span class="sxs-lookup"><span data-stu-id="c56c6-195">From the duration list, select a duration</span></span>
   
    <span data-ttu-id="c56c6-196">b.</span><span class="sxs-lookup"><span data-stu-id="c56c6-196">b.</span></span> <span data-ttu-id="c56c6-197">Dans la barre inférieure, cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="c56c6-197">On the bottom bar, click **Save**.</span></span>
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/10.png)
   
    <span data-ttu-id="c56c6-199">c.</span><span class="sxs-lookup"><span data-stu-id="c56c6-199">c.</span></span> <span data-ttu-id="c56c6-200">Copiez la valeur de la clé.</span><span class="sxs-lookup"><span data-stu-id="c56c6-200">Copy the key value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c56c6-201">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c56c6-201">Next Steps</span></span>
* <span data-ttu-id="c56c6-202">Vous souhaitez accéder aux données de l’API de création de rapports Azure AD par programme ?</span><span class="sxs-lookup"><span data-stu-id="c56c6-202">Would you like to access the data from the Azure AD reporting API in a programmatic manner?</span></span> <span data-ttu-id="c56c6-203">Consultez [Prise en main de l’API de création de rapports Azure Active Directory](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="c56c6-203">Check out [Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="c56c6-204">Si vous souhaitez en savoir plus sur la création de rapports Azure Active Directory, consultez le [Guide Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="c56c6-204">If you would like to find out more about Azure Active Directory reporting, see the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

