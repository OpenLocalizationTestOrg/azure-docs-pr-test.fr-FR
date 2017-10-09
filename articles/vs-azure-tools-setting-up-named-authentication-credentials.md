---
title: "aaaSetting des nommé identification | Documents Microsoft"
description: "Découvrez comment les informations d’identification de tootooprovide que Visual Studio peut utiliser tooauthenticate demandes tooAzure toopublish un tooAzure de l’application à partir de Visual Studio ou toomonitor existant service cloud... "
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
ms.openlocfilehash: 3cc147a2f7a3e766293ca282f56078cf24281346
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-named-authentication-credentials"></a><span data-ttu-id="92950-103">Configuration des informations d’authentification nommées</span><span class="sxs-lookup"><span data-stu-id="92950-103">Setting Up Named Authentication Credentials</span></span>
<span data-ttu-id="92950-104">toopublish un tooAzure de l’application à partir de Visual Studio ou toomonitor un service cloud existant, vous devez fournir les informations d’identification que Visual Studio peut utiliser tooauthenticate demande tooAzure.</span><span class="sxs-lookup"><span data-stu-id="92950-104">toopublish an application tooAzure from Visual Studio or toomonitor an existing cloud service, you must provide credentials that Visual Studio can use tooauthenticate requests tooAzure.</span></span> <span data-ttu-id="92950-105">Il existe plusieurs emplacements dans Visual Studio où vous pouvez vous connecter tooprovide ces informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="92950-105">There are several places in Visual Studio where you can sign in tooprovide these credentials.</span></span> <span data-ttu-id="92950-106">Par exemple, vous pouvez ouvrir à partir de l’Explorateur de serveurs de hello, le menu contextuel hello hello **Azure** nœud et choisissez **connecter tooMicrosoft abonnement Azure...** . Lorsque vous vous connectez, informations d’abonnement hello associées à votre compte Azure sont disponibles dans Visual Studio, et rien de plus, que vous avez toodo.</span><span class="sxs-lookup"><span data-stu-id="92950-106">For example, from hello Server Explorer, you can open hello shortcut menu for hello **Azure** node and choose **Connect tooMicrosoft Azure Subscription...**. When you sign in, hello subscription information associated with your Azure account is available in Visual Studio, and there is nothing more you have toodo.</span></span>

<span data-ttu-id="92950-107">Windows Azure Tools prend également en charge un moyen plus anciens de fournir des informations d’identification, à l’aide de hello abonnement (fichier .publishsettings).</span><span class="sxs-lookup"><span data-stu-id="92950-107">Azure Tools also supports an older way of providing credentials, using hello subscription file (.publishsettings file).</span></span> <span data-ttu-id="92950-108">Cette rubrique explique cette méthode, qui est toujours prise en charge dans le kit de développement logiciel (SDK) Azure 2.2.</span><span class="sxs-lookup"><span data-stu-id="92950-108">This topic describes this method, which is still supported in Azure SDK 2.2.</span></span>

<span data-ttu-id="92950-109">Hello éléments suivants est requis pour l’authentification tooAzure :</span><span class="sxs-lookup"><span data-stu-id="92950-109">hello following items are required for authentication tooAzure:</span></span>

* <span data-ttu-id="92950-110">Votre ID d’abonnement</span><span class="sxs-lookup"><span data-stu-id="92950-110">Your subscription ID</span></span>
* <span data-ttu-id="92950-111">Un certificat X.509 v3 valide</span><span class="sxs-lookup"><span data-stu-id="92950-111">A valid X.509 v3 certificate</span></span>

> [!NOTE]
> <span data-ttu-id="92950-112">la longueur de clé du certificat X.509 v3 de hello Hello doit être au moins 2 048 bits.</span><span class="sxs-lookup"><span data-stu-id="92950-112">hello length of hello X.509 v3 certificate's key must be at least 2048 bits.</span></span> <span data-ttu-id="92950-113">Azure rejette les certificats qui ne répondent pas à cette exigence ou qui ne sont pas valides.</span><span class="sxs-lookup"><span data-stu-id="92950-113">Azure will reject any certificate that doesn’t meet this requirement or that isn’t valid.</span></span>
>
>

<span data-ttu-id="92950-114">Visual Studio utilise votre ID d’abonnement avec les données de certificat hello comme informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="92950-114">Visual Studio uses your subscription ID together with hello certificate data as credentials.</span></span> <span data-ttu-id="92950-115">les informations d’identification appropriées Hello sont référencées dans hello abonnement (fichier .publishsettings), qui contient une clé publique pour le certificat de hello.</span><span class="sxs-lookup"><span data-stu-id="92950-115">hello appropriate credentials are referenced in hello subscription file (.publishsettings file), which contains a public key for hello certificate.</span></span> <span data-ttu-id="92950-116">fichier d’abonnement Hello peut contenir des informations d’identification pour plusieurs abonnements.</span><span class="sxs-lookup"><span data-stu-id="92950-116">hello subscription file can contain credentials for more than one subscription.</span></span>

<span data-ttu-id="92950-117">Vous pouvez modifier les informations d’abonnement hello de hello **nouveau/modifier l’abonnement** boîte de dialogue, comme expliqué plus loin dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="92950-117">You can edit hello subscription information from hello **New/Edit Subscription** dialog box, as explained later in this topic.</span></span>

<span data-ttu-id="92950-118">Si vous voulez toocreate un certificat vous-même, vous pouvez faire référence à des instructions toohello dans [créer et télécharger un certificat de gestion pour Azure](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx) , puis téléchargez manuellement hello certificat toohello [portail Azure classic ](http://go.microsoft.com/fwlink/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="92950-118">If you want toocreate a certificate yourself, you can refer toohello instructions in [Create and Upload a Management Certificate for Azure](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx) and then manually upload hello certificate toohello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span>

> [!NOTE]
> <span data-ttu-id="92950-119">Ces informations d’identification que Visual Studio requiert toomanage que vos services cloud ne sont pas hello les mêmes informations d’identification qui sont requis tooauthenticate une demande auprès des services de stockage Azure hello.</span><span class="sxs-lookup"><span data-stu-id="92950-119">These credentials that Visual Studio requires toomanage your cloud services aren’t hello same credentials that are required tooauthenticate a request against hello Azure storage services.</span></span>
>
>

## <a name="import-set-up-or-edit-authentication-credentials-in-visual-studio"></a><span data-ttu-id="92950-120">Importer, configurer ou modifier des informations d’authentification dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="92950-120">Import, set up, or edit authentication credentials in Visual Studio</span></span>
<span data-ttu-id="92950-121">Vous pouvez importer, configurer ou modifier vos informations d’identification d’authentification Bonjour **nouvel abonnement** boîte de dialogue qui s’affiche si vous effectuez hello suivant l’action :</span><span class="sxs-lookup"><span data-stu-id="92950-121">You can import, set up, or modify your authentication credentials in hello **New Subscription** dialog box, which appears if you perform hello following action:</span></span>

* <span data-ttu-id="92950-122">Dans **l’Explorateur de serveurs**, ouvrez hello sur le menu contextuel hello **Azure** nœud, choisissez **gérer et filtrer les abonnements...** , choisissez hello **certificats** onglet et effectuez l’une des manières suivantes les hello :</span><span class="sxs-lookup"><span data-stu-id="92950-122">In **Server Explorer**, open hello shortcut menu for hello **Azure** node, choose **Manage and Filter Subscriptions...**, choose hello **Certificates** tab, and do one of hello following:</span></span>

    * <span data-ttu-id="92950-123">Choisissez **importer** boîte de dialogue Importer les abonnements Microsoft Azure de hello tooopen où vous pouvez télécharger des fichiers d’abonnements hello pour hello actuellement chargés d’abonnement, parcourir tooits emplacement de téléchargement, puis l’importer pour une utilisation dans authentification.</span><span class="sxs-lookup"><span data-stu-id="92950-123">Choose **Import** tooopen hello Import Microsoft Azure Subscriptions dialog where you can download hello  subscriptions file for hello currently loaded subscription, browse tooits download location, and then import it for use in authentication.</span></span>
    * <span data-ttu-id="92950-124">Choisissez **nouveau** boîte de dialogue Nouvel abonnement de hello tooopen où vous pouvez configurer un nouvel abonnement pour utiliser l’authentification.</span><span class="sxs-lookup"><span data-stu-id="92950-124">Choose **New** tooopen hello New Subscription dialog where you can set up a new subscription for use in authentication.</span></span>
    * <span data-ttu-id="92950-125">Choisissez **modifier** (après le choix de votre abonnement) boîte de dialogue Modifier un abonnement de hello tooopen où vous pouvez modifier un abonnement existant pour une utilisation dans l’authentification.</span><span class="sxs-lookup"><span data-stu-id="92950-125">Choose **Edit** (after choosing your active subscription) tooopen hello Edit Subscription dialog where you can edit an existing subscription for use in authentication.</span></span> 

<span data-ttu-id="92950-126">Hello procédure suivante suppose que hello **nouvel abonnement** boîte de dialogue est ouverte.</span><span class="sxs-lookup"><span data-stu-id="92950-126">hello following procedure assumes that hello **New Subscription** dialog box is open.</span></span>

### <a name="tooset-up-authentication-credentials-in-visual-studio"></a><span data-ttu-id="92950-127">tooset des informations d’identification de l’authentification dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="92950-127">tooset up authentication credentials in Visual Studio</span></span>
1. <span data-ttu-id="92950-128">Bonjour **sélectionner un certificat existant** pour la liste d’authentification, choisissez un certificat.</span><span class="sxs-lookup"><span data-stu-id="92950-128">In hello **Select an existing certificate** for authentication list, choose a certificate.</span></span>
2. <span data-ttu-id="92950-129">Choisissez hello **chemin d’accès complet de copie hello** lien.</span><span class="sxs-lookup"><span data-stu-id="92950-129">Choose hello **Copy hello full path** link.</span></span> <span data-ttu-id="92950-130">chemin d’accès de Hello pour le certificat hello (fichier .cer) est copié toohello du Presse-papiers.</span><span class="sxs-lookup"><span data-stu-id="92950-130">hello path for hello certificate (.cer file) is copied toohello Clipboard.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="92950-131">toopublish votre application Windows Azure à partir de Visual Studio, vous devez télécharger ce certificat toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="92950-131">toopublish your Azure application from Visual Studio, you must upload this certificate toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
   >
   >
3. <span data-ttu-id="92950-132">tooupload hello certificat toohello portail Azure :</span><span class="sxs-lookup"><span data-stu-id="92950-132">tooupload hello certificate toohello Azure portal:</span></span>

   1. <span data-ttu-id="92950-133">Ouvrez hello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="92950-133">Open hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
   2. <span data-ttu-id="92950-134">Si vous y êtes invité, connectez-vous au portail de toohello, puis accédez trop**paramètres**, **certificats de gestion**.</span><span class="sxs-lookup"><span data-stu-id="92950-134">If prompted, sign in toohello portal and then navigate too**Settings**, **Management Certificates**.</span></span>
   3. <span data-ttu-id="92950-135">Dans le volet de certificats de gestion hello, choisissez **télécharger**.</span><span class="sxs-lookup"><span data-stu-id="92950-135">In hello Management certificates pane, choose **Upload**.</span></span>
   4. <span data-ttu-id="92950-136">Sélectionnez votre abonnement Azure, collez hello chemin d’accès complet de fichier .cer hello que vous venez de créée, puis choisissez **télécharger**.</span><span class="sxs-lookup"><span data-stu-id="92950-136">Select your Azure subscription, paste hello full path of hello .cer file that you just created, and choose **Upload**.</span></span>
