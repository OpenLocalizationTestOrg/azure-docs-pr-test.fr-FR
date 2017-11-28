---
title: "Configuration des informations d’authentification nommées | Microsoft Docs"
description: "Découvrez comment fournir des informations d’identification que Visual Studio pourra utiliser pour authentifier les demandes effectuées auprès d’Azure dans le cadre de la publication d’une application dans Azure à partir de Visual Studio, ou de l’analyse d’un service cloud existant. "
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 61570907-42a1-40e8-bcd6-952b21a55786
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/22/2017
ms.author: kraigb
ms.openlocfilehash: c486676a70e195ec85ad40540ea4b7caaa86bc48
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="setting-up-named-authentication-credentials"></a><span data-ttu-id="71d57-103">Configuration des informations d’authentification nommées</span><span class="sxs-lookup"><span data-stu-id="71d57-103">Setting Up Named Authentication Credentials</span></span>
<span data-ttu-id="71d57-104">Pour publier une application dans Azure à partir de Visual Studio, ou pour analyser un service cloud existant, vous devez fournir des informations d’identification que Visual Studio pourra utiliser pour authentifier les demandes effectuées auprès d’Azure.</span><span class="sxs-lookup"><span data-stu-id="71d57-104">To publish an application to Azure from Visual Studio or to monitor an existing cloud service, you must provide credentials that Visual Studio can use to authenticate requests to Azure.</span></span> <span data-ttu-id="71d57-105">Il existe plusieurs emplacements dans Visual Studio à partir desquels vous pouvez vous connecter pour fournir ces informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="71d57-105">There are several places in Visual Studio where you can sign in to provide these credentials.</span></span> <span data-ttu-id="71d57-106">Par exemple, à partir de l’Explorateur de serveurs, vous pouvez ouvrir le menu contextuel du nœud **Azure**, puis sélectionner **Se connecter à Abonnement Microsoft Azure...**. Quand vous vous connectez, les informations d’abonnement associées à votre compte Azure sont disponibles dans Visual Studio. Vous n’avez donc rien à faire de plus.</span><span class="sxs-lookup"><span data-stu-id="71d57-106">For example, from the Server Explorer, you can open the shortcut menu for the **Azure** node and choose **Connect to Microsoft Azure Subscription...**. When you sign in, the subscription information associated with your Azure account is available in Visual Studio, and there is nothing more you have to do.</span></span>

<span data-ttu-id="71d57-107">Les outils Azure prennent également en charge une ancienne méthode d’authentification, qui est l’utilisation du fichier d’abonnement (fichier .publishsettings).</span><span class="sxs-lookup"><span data-stu-id="71d57-107">Azure Tools also supports an older way of providing credentials, using the subscription file (.publishsettings file).</span></span> <span data-ttu-id="71d57-108">Cette rubrique explique cette méthode, qui est toujours prise en charge dans le kit de développement logiciel (SDK) Azure 2.2.</span><span class="sxs-lookup"><span data-stu-id="71d57-108">This topic describes this method, which is still supported in Azure SDK 2.2.</span></span>

<span data-ttu-id="71d57-109">Les éléments suivants sont indispensables pour l’authentification dans Azure :</span><span class="sxs-lookup"><span data-stu-id="71d57-109">The following items are required for authentication to Azure:</span></span>

* <span data-ttu-id="71d57-110">Votre ID d’abonnement</span><span class="sxs-lookup"><span data-stu-id="71d57-110">Your subscription ID</span></span>
* <span data-ttu-id="71d57-111">Un certificat X.509 v3 valide</span><span class="sxs-lookup"><span data-stu-id="71d57-111">A valid X.509 v3 certificate</span></span>

> [!NOTE]
> <span data-ttu-id="71d57-112">La longueur de la clé du certificat X.509 v3 doit être de 2 048 bits au minimum.</span><span class="sxs-lookup"><span data-stu-id="71d57-112">The length of the X.509 v3 certificate's key must be at least 2048 bits.</span></span> <span data-ttu-id="71d57-113">Azure rejette les certificats qui ne répondent pas à cette exigence ou qui ne sont pas valides.</span><span class="sxs-lookup"><span data-stu-id="71d57-113">Azure will reject any certificate that doesn’t meet this requirement or that isn’t valid.</span></span>
>
>

<span data-ttu-id="71d57-114">Visual Studio utilise votre ID d’abonnement et les données du certificat comme informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="71d57-114">Visual Studio uses your subscription ID together with the certificate data as credentials.</span></span> <span data-ttu-id="71d57-115">Les informations d’identification sont référencées dans le fichier d’abonnement (fichier .publishsettings), qui contient une clé publique pour le certificat.</span><span class="sxs-lookup"><span data-stu-id="71d57-115">The appropriate credentials are referenced in the subscription file (.publishsettings file), which contains a public key for the certificate.</span></span> <span data-ttu-id="71d57-116">Le fichier d’abonnement peut contenir des informations d’identification pour plusieurs abonnements.</span><span class="sxs-lookup"><span data-stu-id="71d57-116">The subscription file can contain credentials for more than one subscription.</span></span>

<span data-ttu-id="71d57-117">Vous pouvez modifier les informations d’abonnement à partir de la boîte de dialogue **Modifier l’abonnement/Nouvel abonnement** , comme expliqué plus loin dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="71d57-117">You can edit the subscription information from the **New/Edit Subscription** dialog box, as explained later in this topic.</span></span>

<span data-ttu-id="71d57-118">Si vous souhaitez créer vous-même un certificat, vous pouvez consulter les instructions fournies dans [Créer et charger un certificat de gestion pour Azure](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx), puis charger manuellement le certificat vers le [portail Azure Classic](http://go.microsoft.com/fwlink/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="71d57-118">If you want to create a certificate yourself, you can refer to the instructions in [Create and Upload a Management Certificate for Azure](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx) and then manually upload the certificate to the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span>

> [!NOTE]
> <span data-ttu-id="71d57-119">Les informations d’identification dont Visual Studio a besoin pour gérer vos services cloud ne sont pas les mêmes que celles nécessaires pour authentifier une demande effectuée auprès des services de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="71d57-119">These credentials that Visual Studio requires to manage your cloud services aren’t the same credentials that are required to authenticate a request against the Azure storage services.</span></span>
>
>

## <a name="import-set-up-or-edit-authentication-credentials-in-visual-studio"></a><span data-ttu-id="71d57-120">Importer, configurer ou modifier des informations d’authentification dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="71d57-120">Import, set up, or edit authentication credentials in Visual Studio</span></span>
<span data-ttu-id="71d57-121">Vous pouvez également importer, configurer ou modifier vos informations d’authentification à partir de la boîte de dialogue **Nouvel abonnement** qui s’affiche quand vous effectuez l’action suivante :</span><span class="sxs-lookup"><span data-stu-id="71d57-121">You can import, set up, or modify your authentication credentials in the **New Subscription** dialog box, which appears if you perform the following action:</span></span>

* <span data-ttu-id="71d57-122">Dans l’**Explorateur de serveurs**, ouvrez le menu contextuel du nœud **Azure**, choisissez **Gérer et filtrer les abonnements...**, sélectionnez l’onglet **Certificats**, puis effectuez une des actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="71d57-122">In **Server Explorer**, open the shortcut menu for the **Azure** node, choose **Manage and Filter Subscriptions...**, choose the **Certificates** tab, and do one of the following:</span></span>

    * <span data-ttu-id="71d57-123">Choisissez **Importer** pour ouvrir la boîte de dialogue Importer les abonnements Microsoft Azure, où vous pouvez télécharger le fichier d’abonnements pour l’abonnement actuellement chargé. Accédez à son emplacement de téléchargement, puis importez-le pour l’utiliser pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="71d57-123">Choose **Import** to open the Import Microsoft Azure Subscriptions dialog where you can download the  subscriptions file for the currently loaded subscription, browse to its download location, and then import it for use in authentication.</span></span>
    * <span data-ttu-id="71d57-124">Choisissez **Nouveau** pour ouvrir la boîte de dialogue Nouvel abonnement, dans laquelle vous pouvez configurer un nouvel abonnement à utiliser pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="71d57-124">Choose **New** to open the New Subscription dialog where you can set up a new subscription for use in authentication.</span></span>
    * <span data-ttu-id="71d57-125">Choisissez **Modifier** (après le choix de votre abonnement) pour ouvrir la boîte de dialogue Modifier l’abonnement, où vous pouvez modifier un abonnement existant pour une utilisation pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="71d57-125">Choose **Edit** (after choosing your active subscription) to open the Edit Subscription dialog where you can edit an existing subscription for use in authentication.</span></span> 

<span data-ttu-id="71d57-126">La procédure suivante suppose que la boîte de dialogue **Nouvel abonnement** est ouverte.</span><span class="sxs-lookup"><span data-stu-id="71d57-126">The following procedure assumes that the **New Subscription** dialog box is open.</span></span>

### <a name="to-set-up-authentication-credentials-in-visual-studio"></a><span data-ttu-id="71d57-127">Pour modifier ou exporter des informations d’authentification dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="71d57-127">To set up authentication credentials in Visual Studio</span></span>
1. <span data-ttu-id="71d57-128">Dans la liste **Sélectionnez un certificat existant pour l’authentification** , choisissez un certificat.</span><span class="sxs-lookup"><span data-stu-id="71d57-128">In the **Select an existing certificate** for authentication list, choose a certificate.</span></span>
2. <span data-ttu-id="71d57-129">Cliquez sur le lien **Copier le chemin d’accès complet**.</span><span class="sxs-lookup"><span data-stu-id="71d57-129">Choose the **Copy the full path** link.</span></span> <span data-ttu-id="71d57-130">Le chemin d’accès du certificat (fichier .cer) est copié dans le Presse-papiers.</span><span class="sxs-lookup"><span data-stu-id="71d57-130">The path for the certificate (.cer file) is copied to the Clipboard.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="71d57-131">Pour publier votre application Azure à partir de Visual Studio, vous devrez charger ce certificat vers le [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="71d57-131">To publish your Azure application from Visual Studio, you must upload this certificate to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
   >
   >
3. <span data-ttu-id="71d57-132">Pour télécharger le certificat sur le portail Azure :</span><span class="sxs-lookup"><span data-stu-id="71d57-132">To upload the certificate to the Azure portal:</span></span>

   1. <span data-ttu-id="71d57-133">Ouvrez le [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="71d57-133">Open the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
   2. <span data-ttu-id="71d57-134">Si vous y êtes invité, connectez-vous au portail, puis accédez à **Paramètres**, **Certificats de gestion**.</span><span class="sxs-lookup"><span data-stu-id="71d57-134">If prompted, sign in to the portal and then navigate to **Settings**, **Management Certificates**.</span></span>
   3. <span data-ttu-id="71d57-135">Dans le volet Certificats de gestion, choisissez **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="71d57-135">In the Management certificates pane, choose **Upload**.</span></span>
   4. <span data-ttu-id="71d57-136">Sélectionnez votre abonnement Azure, collez le chemin d’accès complet du fichier .cer que vous venez de créer, puis choisissez **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="71d57-136">Select your Azure subscription, paste the full path of the .cer file that you just created, and choose **Upload**.</span></span>
