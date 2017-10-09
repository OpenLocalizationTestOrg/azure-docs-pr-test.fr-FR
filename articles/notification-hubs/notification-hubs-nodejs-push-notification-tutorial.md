---
title: aaaSending des notifications de push avec Azure Notification Hubs et Node.js
description: "Découvrez comment toouse concentrateurs de Notification toosend des notifications push à partir d’une application Node.js."
keywords: notification push,notifications push,node.js push, ios push
services: notification-hubs
documentationcenter: nodejs
author: ysxu
manager: erikre
editor: 
ms.assetid: ded4749c-6c39-4ff8-b2cf-1927b3e92f93
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 10/25/2016
ms.author: yuaxu
ms.openlocfilehash: 151d224fa6dd07e4acdc3a4887c4e95ee03168c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-and-nodejs"></a><span data-ttu-id="80d61-104">Envoi de notifications Push avec Azure Notification Hubs et Node.js</span><span class="sxs-lookup"><span data-stu-id="80d61-104">Sending push notifications with Azure Notification Hubs and Node.js</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

## <a name="overview"></a><span data-ttu-id="80d61-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="80d61-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="80d61-106">toocomplete ce didacticiel, vous devez disposer d’un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="80d61-106">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="80d61-107">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="80d61-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="80d61-108">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs).</span><span class="sxs-lookup"><span data-stu-id="80d61-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs).</span></span>
> 
> 

<span data-ttu-id="80d61-109">Ce guide vous explique comment toosend push notifications aide hello d’Azure Notification Hubs directement à partir d’une application Node.js.</span><span class="sxs-lookup"><span data-stu-id="80d61-109">This guide will show you how toosend push notifications with hello help of Azure Notification Hubs directly from a Node.js application.</span></span> 

<span data-ttu-id="80d61-110">Hello scénarios couverts : envoi tooapplications de notifications push sur hello suivant plateformes</span><span class="sxs-lookup"><span data-stu-id="80d61-110">hello scenarios covered include sending push notifications tooapplications on hello following platforms:</span></span>

* <span data-ttu-id="80d61-111">Android</span><span class="sxs-lookup"><span data-stu-id="80d61-111">Android</span></span>
* <span data-ttu-id="80d61-112">iOS</span><span class="sxs-lookup"><span data-stu-id="80d61-112">iOS</span></span>
* <span data-ttu-id="80d61-113">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="80d61-113">Windows Phone</span></span>
* <span data-ttu-id="80d61-114">Plateforme Windows universelle</span><span class="sxs-lookup"><span data-stu-id="80d61-114">Universal Windows Platform</span></span> 

<span data-ttu-id="80d61-115">Pour plus d’informations sur les concentrateurs de notification, consultez hello [étapes](#next) section.</span><span class="sxs-lookup"><span data-stu-id="80d61-115">For more information on notification hubs, see hello [Next Steps](#next) section.</span></span>

## <a name="what-are-notification-hubs"></a><span data-ttu-id="80d61-116">Présentation de Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="80d61-116">What are Notification Hubs?</span></span>
<span data-ttu-id="80d61-117">Azure Notification Hubs fournit une infrastructure facile à utiliser, multiplateforme et évolutive pour l’envoi des périphériques toomobile de notifications push.</span><span class="sxs-lookup"><span data-stu-id="80d61-117">Azure Notification Hubs provide an easy-to-use, multi-platform, scalable infrastructure for sending push notifications toomobile devices.</span></span> <span data-ttu-id="80d61-118">Pour plus d’informations sur l’infrastructure de service hello, consultez hello [Azure Notification Hubs](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx) page.</span><span class="sxs-lookup"><span data-stu-id="80d61-118">For details on hello service infrastructure, see hello [Azure Notification Hubs](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx) page.</span></span>

## <a name="create-a-nodejs-application"></a><span data-ttu-id="80d61-119">Création d'une application Node.js</span><span class="sxs-lookup"><span data-stu-id="80d61-119">Create a Node.js Application</span></span>
<span data-ttu-id="80d61-120">Hello première étape de ce didacticiel crée une nouvelle application Node.js vide.</span><span class="sxs-lookup"><span data-stu-id="80d61-120">hello first step in this tutorial is creating a new blank Node.js application.</span></span> <span data-ttu-id="80d61-121">Pour obtenir des instructions sur la création d’une application Node.js, consultez [créer et déployer un tooAzure d’application Node.js Site Web][nodejswebsite], [Service de cloud computing Node.js] [ Node.js Cloud Service] à l’aide de Windows PowerShell, ou [Site Web avec WebMatrix].</span><span class="sxs-lookup"><span data-stu-id="80d61-121">For instructions on creating a Node.js application, see [Create and deploy a Node.js application tooAzure Web Site][nodejswebsite], [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell, or [Web Site with WebMatrix].</span></span>

## <a name="configure-your-application-toouse-notification-hubs"></a><span data-ttu-id="80d61-122">Configurer votre Application tooUse Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="80d61-122">Configure Your Application tooUse Notification Hubs</span></span>
<span data-ttu-id="80d61-123">toouse Azure Notification Hubs, vous devez toodownload et utilisez hello Node.js [package azure](https://www.npmjs.com/package/azure), qui inclut un ensemble prédéfini de bibliothèques d’assistance qui communiquent avec les services de REST de notification push hello.</span><span class="sxs-lookup"><span data-stu-id="80d61-123">toouse Azure Notification Hubs, you need toodownload and use hello Node.js [azure package](https://www.npmjs.com/package/azure), which includes a built-in set of helper libraries that communicate with hello push notification REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="80d61-124">Utiliser le Gestionnaire de Package de nœud (NPM) tooobtain hello package</span><span class="sxs-lookup"><span data-stu-id="80d61-124">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="80d61-125">Utiliser une interface de ligne de commande comme **PowerShell** (Windows), **Terminal** (Mac), ou **Bash** (Linux) et accédez dossier toohello où vous avez créé votre application vide .</span><span class="sxs-lookup"><span data-stu-id="80d61-125">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Linux) and navigate toohello folder where you created your blank application.</span></span>
2. <span data-ttu-id="80d61-126">Type **npm installer azure-sb** dans la fenêtre de commande hello.</span><span class="sxs-lookup"><span data-stu-id="80d61-126">Type **npm install azure-sb** in hello command window.</span></span>
3. <span data-ttu-id="80d61-127">Vous pouvez exécuter manuellement hello **ls** ou **dir** tooverify de commande qui un **nœud\_modules** dossier a été créé.</span><span class="sxs-lookup"><span data-stu-id="80d61-127">You can manually run hello **ls** or **dir** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="80d61-128">Dans ce dossier, recherche hello **azure** package qui contient les bibliothèques hello vous devez tooaccess hello Hub de Notification.</span><span class="sxs-lookup"><span data-stu-id="80d61-128">Inside that folder, find hello **azure** package, which contains hello libraries you need tooaccess hello Notification Hub.</span></span>

> [!NOTE]
> <span data-ttu-id="80d61-129">Plus d’informations sur l’installation NPM sur officielle de hello [NPM blog](http://blog.npmjs.org/post/85484771375/how-to-install-npm).</span><span class="sxs-lookup"><span data-stu-id="80d61-129">You can learn more about installing NPM on hello official [NPM blog](http://blog.npmjs.org/post/85484771375/how-to-install-npm).</span></span> 
> 
> 

### <a name="import-hello-module"></a><span data-ttu-id="80d61-130">Module d’importation hello</span><span class="sxs-lookup"><span data-stu-id="80d61-130">Import hello module</span></span>
<span data-ttu-id="80d61-131">À l’aide d’un éditeur de texte, ajoutez hello suivant en haut de toohello de hello **server.js** fichier de l’application hello :</span><span class="sxs-lookup"><span data-stu-id="80d61-131">Using a text editor, add hello following toohello top of hello **server.js** file of hello application:</span></span>

    var azure = require('azure');

### <a name="setup-an-azure-notification-hub-connection"></a><span data-ttu-id="80d61-132">Configuration d’une connexion Azure Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="80d61-132">Setup an Azure Notification Hub connection</span></span>
<span data-ttu-id="80d61-133">Hello **NotificationHubService** objet vous permet de travailler avec des concentrateurs de notification.</span><span class="sxs-lookup"><span data-stu-id="80d61-133">hello **NotificationHubService** object lets you work with notification hubs.</span></span> <span data-ttu-id="80d61-134">Hello de code suivant crée un **NotificationHubService** objet pour le hub de notification hello nommé **hubname**.</span><span class="sxs-lookup"><span data-stu-id="80d61-134">hello following code creates a **NotificationHubService** object for hello nofication hub named **hubname**.</span></span> <span data-ttu-id="80d61-135">Ajoutez-le haut hello Hello **server.js** fichier, après le module de hello instruction tooimport hello azure :</span><span class="sxs-lookup"><span data-stu-id="80d61-135">Add it near hello top of hello **server.js** file, after hello statement tooimport hello azure module:</span></span>

    var notificationHubService = azure.createNotificationHubService('hubname','connectionstring');

<span data-ttu-id="80d61-136">Hello connexion **connectionstring** peut être obtenue à partir de hello [portail Azure] en effectuant hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="80d61-136">hello connection **connectionstring** value can be obtained from hello [Azure Portal] by performing hello following steps:</span></span>

1. <span data-ttu-id="80d61-137">Dans le volet de navigation gauche hello, cliquez sur **Parcourir**.</span><span class="sxs-lookup"><span data-stu-id="80d61-137">In hello left navigation pane, click **Browse**.</span></span>
2. <span data-ttu-id="80d61-138">Sélectionnez **concentrateurs de Notification**, puis rechercher hello hub vous souhaitez toouse pour l’exemple hello et.</span><span class="sxs-lookup"><span data-stu-id="80d61-138">Select **Notification Hubs**, and then find hello hub you wish toouse for hello sample.</span></span> <span data-ttu-id="80d61-139">Vous pouvez faire référence toohello [Windows Store prise en main de didacticiel](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) si vous avez besoin d’aide pour créer un concentrateur de Notification.</span><span class="sxs-lookup"><span data-stu-id="80d61-139">You can refer toohello [Windows Store Getting Started tutorial](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) if you need help creating a new Notification Hub.</span></span>
3. <span data-ttu-id="80d61-140">Sélectionnez **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="80d61-140">Select **Settings**.</span></span>
4. <span data-ttu-id="80d61-141">Cliquez sur **Stratégies d’accès**.</span><span class="sxs-lookup"><span data-stu-id="80d61-141">Click on **Access Policies**.</span></span> <span data-ttu-id="80d61-142">Vous pouvez voir les chaînes de connexion d’accès total et partagé.</span><span class="sxs-lookup"><span data-stu-id="80d61-142">You will see both shared and full access connection strings.</span></span>

![Portail Azure - Notification Hubs](./media/notification-hubs-nodejs-how-to-use-notification-hubs/notification-hubs-portal.png)

> [!NOTE]
> <span data-ttu-id="80d61-144">Vous pouvez également récupérer la chaîne de connexion hello à l’aide de hello **Get-AzureSbNamespace** applet de commande fournie par [Azure PowerShell](/powershell/azureps-cmdlets-docs) ou hello **afficher d’espace de noms service bus azure** avec Hello [Azure Interface de ligne (Azure)](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="80d61-144">You can also retrieve hello connection string using hello **Get-AzureSbNamespace** cmdlet provided by [Azure PowerShell](/powershell/azureps-cmdlets-docs) or hello **azure sb namespace show** command with hello [Azure Command-Line Interface (Azure CLI)](../cli-install-nodejs.md).</span></span>
> 
> 

## <a name="general-architecture"></a><span data-ttu-id="80d61-145">Architecture générale</span><span class="sxs-lookup"><span data-stu-id="80d61-145">General architecture</span></span>
<span data-ttu-id="80d61-146">Hello **NotificationHubService** objet expose hello suivant des instances d’objet pour l’envoi de push notifications toospecific appareils et applications :</span><span class="sxs-lookup"><span data-stu-id="80d61-146">hello **NotificationHubService** object exposes hello following object instances for sending push notifications toospecific devices and applications:</span></span>

* <span data-ttu-id="80d61-147">**Android** -utilisez hello **GcmService** objet, qui est disponible à l’adresse **notificationHubService.gcm**</span><span class="sxs-lookup"><span data-stu-id="80d61-147">**Android** - use hello **GcmService** object, which is available at **notificationHubService.gcm**</span></span>
* <span data-ttu-id="80d61-148">**iOS** -utilisez hello **ApnsService** objet, qui est accessible à **notificationHubService.apns**</span><span class="sxs-lookup"><span data-stu-id="80d61-148">**iOS** - use hello **ApnsService** object, which is accessible at **notificationHubService.apns**</span></span>
* <span data-ttu-id="80d61-149">**Windows Phone** -utilisez hello **MpnsService** objet, qui est disponible à l’adresse **notificationHubService.mpns**</span><span class="sxs-lookup"><span data-stu-id="80d61-149">**Windows Phone** - use hello **MpnsService** object, which is available at **notificationHubService.mpns**</span></span>
* <span data-ttu-id="80d61-150">**Plateforme Windows universelle** -utilisez hello **WnsService** objet, qui est disponible à l’adresse **notificationHubService.wns**</span><span class="sxs-lookup"><span data-stu-id="80d61-150">**Universal Windows Platform** - use hello **WnsService** object, which is available at **notificationHubService.wns**</span></span>

### <a name="how-to-send-push-notifications-tooandroid-applications"></a><span data-ttu-id="80d61-151">Comment : envoyer des applications tooAndroid de notifications push</span><span class="sxs-lookup"><span data-stu-id="80d61-151">How to: Send push notifications tooAndroid applications</span></span>
<span data-ttu-id="80d61-152">Hello **GcmService** objet fournit une **envoyer** (méthode) qui peut être utilisés toosend push notifications tooAndroid applications.</span><span class="sxs-lookup"><span data-stu-id="80d61-152">hello **GcmService** object provides a **send** method that can be used toosend push notifications tooAndroid applications.</span></span> <span data-ttu-id="80d61-153">Hello **envoyer** méthode accepte hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="80d61-153">hello **send** method accepts hello following parameters:</span></span>

* <span data-ttu-id="80d61-154">**Balises** -hello identificateur de balise.</span><span class="sxs-lookup"><span data-stu-id="80d61-154">**Tags** - hello tag identifier.</span></span> <span data-ttu-id="80d61-155">Si aucune balise n’est fourni, notification de hello est envoyée tooall clients.</span><span class="sxs-lookup"><span data-stu-id="80d61-155">If no tag is provided, hello notification will be sent tooall clients.</span></span>
* <span data-ttu-id="80d61-156">**Charge utile** -hello JSON ou la charge utile de chaîne brute du message.</span><span class="sxs-lookup"><span data-stu-id="80d61-156">**Payload** - hello message's JSON or raw string payload.</span></span>
* <span data-ttu-id="80d61-157">**Rappel** -hello la fonction de rappel.</span><span class="sxs-lookup"><span data-stu-id="80d61-157">**Callback** - hello callback function.</span></span>

<span data-ttu-id="80d61-158">Pour plus d’informations sur le format de charge utile hello, consultez hello **charge utile** section Hello [implémentation d’un serveur GCM](http://developer.android.com/google/gcm/server.html#payload) document.</span><span class="sxs-lookup"><span data-stu-id="80d61-158">For more information on hello payload format, see hello **Payload** section of hello [Implementing GCM Server](http://developer.android.com/google/gcm/server.html#payload) document.</span></span>

<span data-ttu-id="80d61-159">Hello de code suivant utilise hello **GcmService** instance exposée par hello **NotificationHubService** toosend un tooall de notification push inscrit les clients.</span><span class="sxs-lookup"><span data-stu-id="80d61-159">hello following code uses hello **GcmService** instance exposed by hello **NotificationHubService** toosend a push notification tooall registered clients.</span></span>

    var payload = {
      data: {
        message: 'Hello!'
      }
    };
    notificationHubService.gcm.send(null, payload, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-tooios-applications"></a><span data-ttu-id="80d61-160">Comment : envoyer des applications tooiOS de notifications push</span><span class="sxs-lookup"><span data-stu-id="80d61-160">How to: Send push notifications tooiOS applications</span></span>
<span data-ttu-id="80d61-161">Même comme avec les applications Android décrite ci-dessus, hello **ApnsService** objet fournit une **envoyer** (méthode) qui peut être utilisés toosend push notifications tooiOS applications.</span><span class="sxs-lookup"><span data-stu-id="80d61-161">Same as with Android applications described above, hello **ApnsService** object provides a **send** method that can be used toosend push notifications tooiOS applications.</span></span> <span data-ttu-id="80d61-162">Hello **envoyer** méthode accepte hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="80d61-162">hello **send** method accepts hello following parameters:</span></span>

* <span data-ttu-id="80d61-163">**Balises** -hello identificateur de balise.</span><span class="sxs-lookup"><span data-stu-id="80d61-163">**Tags** - hello tag identifier.</span></span> <span data-ttu-id="80d61-164">Si aucune balise n’est fourni, notification de hello est envoyée tooall clients.</span><span class="sxs-lookup"><span data-stu-id="80d61-164">If no tag is provided, hello notification will be sent tooall clients.</span></span>
* <span data-ttu-id="80d61-165">**Charge utile** - hello JSON du message ou charge utile de la chaîne.</span><span class="sxs-lookup"><span data-stu-id="80d61-165">**Payload** - hello message's JSON or string payload.</span></span>
* <span data-ttu-id="80d61-166">**Rappel** -hello la fonction de rappel.</span><span class="sxs-lookup"><span data-stu-id="80d61-166">**Callback** - hello callback function.</span></span>

<span data-ttu-id="80d61-167">Pour le format de charge utile hello plus d’informations, consultez hello **charge utile de Notification** section Hello [Local et le Guide de programmation de Notification Push](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html) document.</span><span class="sxs-lookup"><span data-stu-id="80d61-167">For more information hello payload format, see hello **Notification Payload** section of hello [Local and Push Notification Programming Guide](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html) document.</span></span>

<span data-ttu-id="80d61-168">Hello de code suivant utilise hello **ApnsService** instance exposée par hello **NotificationHubService** toosend une alerte de message tooall clients :</span><span class="sxs-lookup"><span data-stu-id="80d61-168">hello following code uses hello **ApnsService** instance exposed by hello **NotificationHubService** toosend an alert message tooall clients:</span></span>

    var payload={
        alert: 'Hello!'
      };
    notificationHubService.apns.send(null, payload, function(error){
      if(!error){
         // notification sent
      }
    });

### <a name="how-to-send-push-notifications-toowindows-phone-applications"></a><span data-ttu-id="80d61-169">Comment : envoyer des applications de téléphone tooWindows des notifications push</span><span class="sxs-lookup"><span data-stu-id="80d61-169">How to: Send push notifications tooWindows Phone applications</span></span>
<span data-ttu-id="80d61-170">Hello **MpnsService** objet fournit une **envoyer** méthode qui peut être utilisé toosend push notifications tooWindows applications téléphoniques.</span><span class="sxs-lookup"><span data-stu-id="80d61-170">hello **MpnsService** object provides a **send** method that can be used toosend push notifications tooWindows Phone applications.</span></span> <span data-ttu-id="80d61-171">Hello **envoyer** méthode accepte hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="80d61-171">hello **send** method accepts hello following parameters:</span></span>

* <span data-ttu-id="80d61-172">**Balises** -hello identificateur de balise.</span><span class="sxs-lookup"><span data-stu-id="80d61-172">**Tags** - hello tag identifier.</span></span> <span data-ttu-id="80d61-173">Si aucune balise n’est fourni, notification de hello est envoyée tooall clients.</span><span class="sxs-lookup"><span data-stu-id="80d61-173">If no tag is provided, hello notification will be sent tooall clients.</span></span>
* <span data-ttu-id="80d61-174">**Charge utile** -hello la charge utile XML du message.</span><span class="sxs-lookup"><span data-stu-id="80d61-174">**Payload** - hello message's XML payload.</span></span>
* <span data-ttu-id="80d61-175">**TargetName** - `toast` pour les notifications toast.</span><span class="sxs-lookup"><span data-stu-id="80d61-175">**TargetName** - `toast` for toast notifications.</span></span> <span data-ttu-id="80d61-176">`token` pour les notifications par vignette.</span><span class="sxs-lookup"><span data-stu-id="80d61-176">`token` for tile notifications.</span></span>
* <span data-ttu-id="80d61-177">**Classe de notification** -hello priorité de notification de hello.</span><span class="sxs-lookup"><span data-stu-id="80d61-177">**NotificationClass** - hello priority of hello notification.</span></span> <span data-ttu-id="80d61-178">Consultez hello **éléments d’en-tête HTTP** section Hello [des notifications Push à partir d’un serveur](http://msdn.microsoft.com/library/hh221551.aspx) document pour les valeurs valides.</span><span class="sxs-lookup"><span data-stu-id="80d61-178">See hello **HTTP Header Elements** section of hello [Push notifications from a server](http://msdn.microsoft.com/library/hh221551.aspx) document for valid values.</span></span>
* <span data-ttu-id="80d61-179">**Options** : en-têtes de demande facultatifs.</span><span class="sxs-lookup"><span data-stu-id="80d61-179">**Options** - optional request headers.</span></span>
* <span data-ttu-id="80d61-180">**Rappel** -hello la fonction de rappel.</span><span class="sxs-lookup"><span data-stu-id="80d61-180">**Callback** - hello callback function.</span></span>

<span data-ttu-id="80d61-181">Pour obtenir la liste de valide **TargetName**, **classe de notification** et options d’en-tête, consultez hello [des notifications Push à partir d’un serveur](http://msdn.microsoft.com/library/hh221551.aspx) page.</span><span class="sxs-lookup"><span data-stu-id="80d61-181">For a list of valid **TargetName**, **NotificationClass** and header options, check out hello [Push notifications from a server](http://msdn.microsoft.com/library/hh221551.aspx) page.</span></span>

<span data-ttu-id="80d61-182">Hello suivant l’exemple de code utilise hello **MpnsService** instance exposée par hello **NotificationHubService** toosend une notification toast :</span><span class="sxs-lookup"><span data-stu-id="80d61-182">hello following sample code uses hello **MpnsService** instance exposed by hello **NotificationHubService** toosend a toast push notification:</span></span>

    var payload = '<?xml version="1.0" encoding="utf-8"?><wp:Notification xmlns:wp="WPNotification"><wp:Toast><wp:Text1>string</wp:Text1><wp:Text2>string</wp:Text2></wp:Toast></wp:Notification>';
    notificationHubService.mpns.send(null, payload, 'toast', 22, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-toouniversal-windows-platform-uwp-applications"></a><span data-ttu-id="80d61-183">Comment : envoyer des applications de Windows Platform (UWP) tooUniversal de notifications push</span><span class="sxs-lookup"><span data-stu-id="80d61-183">How to: Send push notifications tooUniversal Windows Platform (UWP) applications</span></span>
<span data-ttu-id="80d61-184">Hello **WnsService** objet fournit une **envoyer** méthode qui peut être des applications de plateforme Windows tooUniversal toosend utilisé push notifications.</span><span class="sxs-lookup"><span data-stu-id="80d61-184">hello **WnsService** object provides a **send** method that can be used toosend push notifications tooUniversal Windows Platform applications.</span></span>  <span data-ttu-id="80d61-185">Hello **envoyer** méthode accepte hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="80d61-185">hello **send** method accepts hello following parameters:</span></span>

* <span data-ttu-id="80d61-186">**Balises** -hello identificateur de balise.</span><span class="sxs-lookup"><span data-stu-id="80d61-186">**Tags** - hello tag identifier.</span></span> <span data-ttu-id="80d61-187">Si aucune balise n’est fourni, notification de hello est envoyée tooall inscrit clients.</span><span class="sxs-lookup"><span data-stu-id="80d61-187">If no tag is provided, hello notification will be sent tooall registered clients.</span></span>
* <span data-ttu-id="80d61-188">**Charge utile** -charge utile du message XML hello.</span><span class="sxs-lookup"><span data-stu-id="80d61-188">**Payload** - hello XML message payload.</span></span>
* <span data-ttu-id="80d61-189">**Type** -hello du type de notification.</span><span class="sxs-lookup"><span data-stu-id="80d61-189">**Type** - hello notification type.</span></span>
* <span data-ttu-id="80d61-190">**Options** : en-têtes de demande facultatifs.</span><span class="sxs-lookup"><span data-stu-id="80d61-190">**Options** - optional request headers.</span></span>
* <span data-ttu-id="80d61-191">**Rappel** -hello la fonction de rappel.</span><span class="sxs-lookup"><span data-stu-id="80d61-191">**Callback** - hello callback function.</span></span>

<span data-ttu-id="80d61-192">Pour obtenir la liste des types et en-têtes de demande valides, consultez [En-têtes de demande et de réponse des services de notifications Push](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx).</span><span class="sxs-lookup"><span data-stu-id="80d61-192">For a list of valid types and request headers, see [Push notification service request and response headers](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx).</span></span>

<span data-ttu-id="80d61-193">Hello de code suivant utilise hello **WnsService** instance exposée par hello **NotificationHubService** toosend une application UWP de toast push notification tooa :</span><span class="sxs-lookup"><span data-stu-id="80d61-193">hello following code uses hello **WnsService** instance exposed by hello **NotificationHubService** toosend a toast push notification tooa UWP app:</span></span>

    var payload = '<toast><visual><binding template="ToastText01"><text id="1">Hello!</text></binding></visual></toast>';
    notificationHubService.wns.send(null, payload , 'wns/toast', function(error){
      if(!error){
         // notification sent
      }
    });

## <a name="next-steps"></a><span data-ttu-id="80d61-194">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="80d61-194">Next Steps</span></span>
<span data-ttu-id="80d61-195">Hello exemple des extraits de code ci-dessus permettent de vous tooeasily build service infrastructure toodeliver push notifications tooa large gamme de périphériques.</span><span class="sxs-lookup"><span data-stu-id="80d61-195">hello sample snippets above allow you tooeasily build service infrastructure toodeliver push notifications tooa wide variety of devices.</span></span> <span data-ttu-id="80d61-196">Maintenant que vous avez appris les notions de base de hello de l’utilisation des concentrateurs de Notification avec node.js, suivez ces liens de toolearn plus d’informations sur la manière d’étendre ces fonctionnalités supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="80d61-196">Now that you've learned hello basics of using Notification Hubs with node.js, follow these links toolearn more about how you can extend these capabilities further.</span></span>

* <span data-ttu-id="80d61-197">Consultez hello référence MSDN pour [Azure Notification Hubs](https://msdn.microsoft.com/library/azure/jj927170.aspx).</span><span class="sxs-lookup"><span data-stu-id="80d61-197">See hello MSDN Reference for [Azure Notification Hubs](https://msdn.microsoft.com/library/azure/jj927170.aspx).</span></span>
* <span data-ttu-id="80d61-198">Visitez hello [Azure SDK pour le nœud] référentiel sur GitHub pour plus d’exemples et les détails d’implémentation.</span><span class="sxs-lookup"><span data-stu-id="80d61-198">Visit hello [Azure SDK for Node] repository on GitHub for more samples and implementation details.</span></span>

[Azure SDK pour le nœud]: https://github.com/WindowsAzure/azure-sdk-for-node
[Next Steps]: #nextsteps
[What are Service Bus Topics and Subscriptions?]: #what-are-service-bus-topics
[Create a Service Namespace]: #create-a-service-namespace
[Obtain hello Default Management Credentials for hello Namespace]: #obtain-default-credentials
[Create a Node.js Application]: #Create_a_Nodejs_Application
[Configure Your Application tooUse Service Bus]: #Configure_Your_Application_to_Use_Service_Bus
[How to: Create a Topic]: #How_to_Create_a_Topic
[How to: Create Subscriptions]: #How_to_Create_Subscriptions
[How to: Send Messages tooa Topic]: #How_to_Send_Messages_to_a_Topic
[How to: Receive Messages from a Subscription]: #How_to_Receive_Messages_from_a_Subscription
[How to: Handle Application Crashes and Unreadable Messages]: #How_to_Handle_Application_Crashes_and_Unreadable_Messages
[How to: Delete Topics and Subscriptions]: #How_to_Delete_Topics_and_Subscriptions
[1]: #Next_Steps
[Topic Concepts]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-topics-01.png
[Azure Classic Portal]: http://manage.windowsazure.com
[image]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-03.png
[2]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-04.png
[3]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-05.png
[4]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-06.png
[5]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-07.png
[SqlFilter.SqlExpression]: http://msdn.microsoft.com/library/windowsazure/microsoft.servicebus.messaging.sqlfilter.sqlexpression.aspx
[Azure Service Bus Notification Hubs]: http://msdn.microsoft.com/library/windowsazure/jj927170.aspx
[SqlFilter]: http://msdn.microsoft.com/library/windowsazure/microsoft.servicebus.messaging.sqlfilter.aspx
[Site Web avec WebMatrix]: /develop/nodejs/tutorials/web-site-with-webmatrix/
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Previous Management Portal]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/previous-portal.png
[nodejswebsite]: /develop/nodejs/tutorials/create-a-website-(mac)/
[Node.js Cloud Service with Storage]: /develop/nodejs/tutorials/web-app-with-storage/
[Node.js Web Application with Storage]: /develop/nodejs/tutorials/web-site-with-storage/
[portail Azure]: https://portal.azure.com
