---
title: "rôles des Services de cloud computing aaaAzure FAQ | Documents Microsoft"
description: "Forum aux questions sur les Services cloud Azure. Répond à certaines questions courantes sur les certificats, les rôles web et les rôles Worker."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: b07a1990e031e60ae919a5f7c636945b89c7d3a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-services-faq"></a><span data-ttu-id="dbb4e-104">Forum aux questions sur les services cloud</span><span class="sxs-lookup"><span data-stu-id="dbb4e-104">Cloud Services FAQ</span></span>
<span data-ttu-id="dbb4e-105">Cet article répond à certaines questions fréquemment posées sur les services cloud Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="dbb4e-105">This article answers some frequently asked questions about Microsoft Azure Cloud Services.</span></span> <span data-ttu-id="dbb4e-106">Vous pouvez aussi visiter hello [Forum aux questions sur Azure prend en charge](http://go.microsoft.com/fwlink/?LinkID=185083) pour plus d’informations de tarification et la prise en charge Azure.</span><span class="sxs-lookup"><span data-stu-id="dbb4e-106">You can also visit hello [Azure Support FAQ](http://go.microsoft.com/fwlink/?LinkID=185083) for general Azure pricing and support information.</span></span> <span data-ttu-id="dbb4e-107">Vous pouvez également consulter hello [page de taille de machine virtuelle de Services Cloud](cloud-services-sizes-specs.md) pour les informations de taille.</span><span class="sxs-lookup"><span data-stu-id="dbb4e-107">You can also consult hello [Cloud Services VM Size page](cloud-services-sizes-specs.md) for size information.</span></span>

## <a name="certificates"></a><span data-ttu-id="dbb4e-108">Certificats</span><span class="sxs-lookup"><span data-stu-id="dbb4e-108">Certificates</span></span>
### <a name="where-should-i-install-my-certificate"></a><span data-ttu-id="dbb4e-109">Où dois-je installer mon certificat ?</span><span class="sxs-lookup"><span data-stu-id="dbb4e-109">Where should I install my certificate?</span></span>
* <span data-ttu-id="dbb4e-110">**My**</span><span class="sxs-lookup"><span data-stu-id="dbb4e-110">**My**</span></span>  
  <span data-ttu-id="dbb4e-111">Certificat d’application avec clé privée (\*.pfx, \*.p12).</span><span class="sxs-lookup"><span data-stu-id="dbb4e-111">Application Certificate with private key (\*.pfx, \*.p12).</span></span>
* <span data-ttu-id="dbb4e-112">**CA**</span><span class="sxs-lookup"><span data-stu-id="dbb4e-112">**CA**</span></span>  
  <span data-ttu-id="dbb4e-113">Tous vos certificats intermédiaires sont stockés dans ce magasin (stratégie et autorités de certification secondaires).</span><span class="sxs-lookup"><span data-stu-id="dbb4e-113">All your intermediate certificates go in this store (Policy and Sub CAs).</span></span>
* <span data-ttu-id="dbb4e-114">**ROOT**</span><span class="sxs-lookup"><span data-stu-id="dbb4e-114">**ROOT**</span></span>  
  <span data-ttu-id="dbb4e-115">magasin d’autorité de certification racine de Hello, afin de votre certificat d’autorité de certification racine principal doit être ici.</span><span class="sxs-lookup"><span data-stu-id="dbb4e-115">hello root CA store, so your main root CA cert should go here.</span></span>

### <a name="i-cant-remove-expired-certificate"></a><span data-ttu-id="dbb4e-116">Impossible de supprimer les certificats expirés</span><span class="sxs-lookup"><span data-stu-id="dbb4e-116">I can't remove expired certificate</span></span>
<span data-ttu-id="dbb4e-117">Azure vous empêche de supprimer un certificat s’il est en cours d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="dbb4e-117">Azure prevents you from removing a certificate while it is in use.</span></span> <span data-ttu-id="dbb4e-118">Vous devez tooeither delete hello déploiement qui utilise le certificat de hello ou mise à jour hello déploiement avec un certificat différent ou renouvelé.</span><span class="sxs-lookup"><span data-stu-id="dbb4e-118">You need tooeither delete hello deployment that uses hello certificate, or update hello deployment with a different or renewed certificate.</span></span>

### <a name="delete-an-expired-certificate"></a><span data-ttu-id="dbb4e-119">Suppression d’un certificat ayant expiré</span><span class="sxs-lookup"><span data-stu-id="dbb4e-119">Delete an expired certificate</span></span>
<span data-ttu-id="dbb4e-120">Tant que certificat de hello n’est pas en cours d’utilisation, vous pouvez utiliser hello [Remove-AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) tooremove d’applet de commande PowerShell un certificat.</span><span class="sxs-lookup"><span data-stu-id="dbb4e-120">As long as hello certificate is not in use, you can use hello [Remove-AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) PowerShell cmdlet tooremove a certificate.</span></span>

### <a name="i-have-expired-certificates-named-windows-azure-service-management-for-extensions"></a><span data-ttu-id="dbb4e-121">Mes certificats Windows Azure Service Management for Extensions ont expiré</span><span class="sxs-lookup"><span data-stu-id="dbb4e-121">I have expired certificates named Windows Azure Service Management for Extensions</span></span>
<span data-ttu-id="dbb4e-122">Ces certificats sont créés chaque fois qu’une extension est ajoutée le service de cloud computing toohello tels que hello extension du Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="dbb4e-122">These certificates are created whenever an extension is added toohello cloud service such as hello Remote Desktop extension.</span></span> <span data-ttu-id="dbb4e-123">Ces certificats sont utilisés uniquement pour chiffrer et déchiffrer la configuration privée d’extension de hello d’hello.</span><span class="sxs-lookup"><span data-stu-id="dbb4e-123">These certificates are only used for encrypting and decrypting hello private configuration of hello extension.</span></span> <span data-ttu-id="dbb4e-124">L’expiration de ces certificats n’a aucune importance.</span><span class="sxs-lookup"><span data-stu-id="dbb4e-124">It does not matter if these certificates expire.</span></span> <span data-ttu-id="dbb4e-125">date d’expiration de Hello n’est pas vérifiée.</span><span class="sxs-lookup"><span data-stu-id="dbb4e-125">hello expiration date is not checked.</span></span>

### <a name="certificates-i-have-deleted-keep-reappearing"></a><span data-ttu-id="dbb4e-126">Les certificats que j’ai supprimés continuent à s’afficher</span><span class="sxs-lookup"><span data-stu-id="dbb4e-126">Certificates I have deleted keep reappearing</span></span>
<span data-ttu-id="dbb4e-127">Ces certificats continuent de s’afficher en raison d’un outil que vous utilisez, comme Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dbb4e-127">These keep reappearing most likely because of a tool you're using, such as Visual Studio.</span></span> <span data-ttu-id="dbb4e-128">Chaque fois que vous vous reconnectez à un outil qui utilise un certificat, il sera à nouveau téléchargé tooAzure.</span><span class="sxs-lookup"><span data-stu-id="dbb4e-128">Whenever you reconnect with a tool that is using a certificate, it will again be uploaded tooAzure.</span></span>

### <a name="my-certificates-keep-disappearing"></a><span data-ttu-id="dbb4e-129">Mes certificats ne cessent de disparaître</span><span class="sxs-lookup"><span data-stu-id="dbb4e-129">My certificates keep disappearing</span></span>
<span data-ttu-id="dbb4e-130">Lorsque l’instance de machine virtuelle hello est recyclé, toutes les modifications locales sont perdues.</span><span class="sxs-lookup"><span data-stu-id="dbb4e-130">When hello virtual machine instance recycles, all local changes are lost.</span></span> <span data-ttu-id="dbb4e-131">Utilisez un [tâche de démarrage](cloud-services-startup-tasks.md) tooinstall certificats toohello virtual machine chaque heure hello démarre.</span><span class="sxs-lookup"><span data-stu-id="dbb4e-131">Use a [startup task](cloud-services-startup-tasks.md) tooinstall certificates toohello virtual machine each time hello role starts.</span></span>

### <a name="i-cannot-find-my-management-certificates-in-hello-portal"></a><span data-ttu-id="dbb4e-132">Impossible de trouver les certificats de gestion dans le portail de hello</span><span class="sxs-lookup"><span data-stu-id="dbb4e-132">I cannot find my management certificates in hello portal</span></span>
<span data-ttu-id="dbb4e-133">[Certificats de gestion](../azure-api-management-certs.md) sont disponibles uniquement dans hello portail classique Azure.</span><span class="sxs-lookup"><span data-stu-id="dbb4e-133">[Management certificates](../azure-api-management-certs.md) are only available in hello Azure Classic Portal.</span></span> <span data-ttu-id="dbb4e-134">portail Azure actuel de Hello n’utilise pas de certificats de gestion.</span><span class="sxs-lookup"><span data-stu-id="dbb4e-134">hello current Azure portal does not use management certificates.</span></span> 

### <a name="how-can-i-disable-a-management-certificate"></a><span data-ttu-id="dbb4e-135">Comment puis-je désactiver un certificat de gestion ?</span><span class="sxs-lookup"><span data-stu-id="dbb4e-135">How can I disable a management certificate?</span></span>
<span data-ttu-id="dbb4e-136">[certificats de gestion](../azure-api-management-certs.md) ne peuvent pas être désactivés.</span><span class="sxs-lookup"><span data-stu-id="dbb4e-136">[Management certificates](../azure-api-management-certs.md) cannot be disabled.</span></span> <span data-ttu-id="dbb4e-137">Vous supprimer via hello portail classique Azure lorsque vous ne souhaitez pas que les toobe plus utilisé.</span><span class="sxs-lookup"><span data-stu-id="dbb4e-137">You delete them through hello Azure Classic Portal when you do not want them toobe used anymore.</span></span>

### <a name="how-do-i-create-an-ssl-certificate-for-a-specific-ip-address"></a><span data-ttu-id="dbb4e-138">Comment créer un certificat SSL pour une adresse IP spécifique ?</span><span class="sxs-lookup"><span data-stu-id="dbb4e-138">How do I create an SSL certificate for a specific IP address?</span></span>
<span data-ttu-id="dbb4e-139">Suivez les instructions de hello Bonjour [créer un didacticiel de certificat](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="dbb4e-139">Follow hello directions in hello [create a certificate tutorial](cloud-services-certs-create.md).</span></span> <span data-ttu-id="dbb4e-140">Utiliser l’adresse IP de hello comme hello nom DNS.</span><span class="sxs-lookup"><span data-stu-id="dbb4e-140">Use hello IP address as hello DNS Name.</span></span>

## <a name="security"></a><span data-ttu-id="dbb4e-141">Sécurité</span><span class="sxs-lookup"><span data-stu-id="dbb4e-141">Security</span></span>
### <a name="disable-ssl-30"></a><span data-ttu-id="dbb4e-142">Désactiver SSL 3.0</span><span class="sxs-lookup"><span data-stu-id="dbb4e-142">Disable SSL 3.0</span></span>
<span data-ttu-id="dbb4e-143">toodisable SSL 3.0 et TLS utilise la sécurité, créez une tâche de démarrage qui est décrit dans ce billet de blog : https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/</span><span class="sxs-lookup"><span data-stu-id="dbb4e-143">toodisable SSL 3.0 and use TLS security, create a startup task which is documented on this blog post: https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/</span></span>

### <a name="add-nosniff-tooyour-website"></a><span data-ttu-id="dbb4e-144">Ajouter **nosniff** tooyour site</span><span class="sxs-lookup"><span data-stu-id="dbb4e-144">Add **nosniff** tooyour website</span></span>
<span data-ttu-id="dbb4e-145">les clients tooprevent à partir de la détection des types MIME de hello, ajoutez un paramètre dans votre *web.config* fichier.</span><span class="sxs-lookup"><span data-stu-id="dbb4e-145">tooprevent clients from sniffing hello MIME types, add a setting in your *web.config* file.</span></span>

```xml
<configuration>
   <system.webServer>
      <httpProtocol>
         <customHeaders>
            <add name="X-Content-Type-Options" value="nosniff" />
         </customHeaders>
      </httpProtocol>
   </system.webServer>
</configuration>
```

<span data-ttu-id="dbb4e-146">Vous pouvez également ajouter ce paramètre dans IIS.</span><span class="sxs-lookup"><span data-stu-id="dbb4e-146">You can also add this as a setting in IIS.</span></span> <span data-ttu-id="dbb4e-147">Suivant de hello d’utilisation de commandes avec hello [tâches courantes de démarrage](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) l’article.</span><span class="sxs-lookup"><span data-stu-id="dbb4e-147">Use hello following command with hello [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) article.</span></span>

```cmd
%windir%\system32\inetsrv\appcmd set config /section:httpProtocol /+customHeaders.[name='X-Content-Type-Options',value='nosniff']
```

### <a name="customize-iis-for-a-web-role"></a><span data-ttu-id="dbb4e-148">Personnaliser IIS pour un rôle web</span><span class="sxs-lookup"><span data-stu-id="dbb4e-148">Customize IIS for a web role</span></span>
<span data-ttu-id="dbb4e-149">Utiliser le script de démarrage IIS hello de hello [tâches courantes de démarrage](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) l’article.</span><span class="sxs-lookup"><span data-stu-id="dbb4e-149">Use hello IIS startup script from hello [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) article.</span></span>

## <a name="scaling"></a><span data-ttu-id="dbb4e-150">Mise à l'échelle</span><span class="sxs-lookup"><span data-stu-id="dbb4e-150">Scaling</span></span>
### <a name="i-cannot-scale-beyond-x-instances"></a><span data-ttu-id="dbb4e-151">Je ne parviens pas à mettre à l’échelle au-delà de X instances</span><span class="sxs-lookup"><span data-stu-id="dbb4e-151">I cannot scale beyond X instances</span></span>
<span data-ttu-id="dbb4e-152">Votre abonnement Azure a une limite de nombre de hello de cœurs que vous pouvez utiliser.</span><span class="sxs-lookup"><span data-stu-id="dbb4e-152">Your Azure Subscription has a limit on hello number of cores you can use.</span></span> <span data-ttu-id="dbb4e-153">Mise à l’échelle ne fonctionnera pas si vous avez utilisé tous les cœurs hello disponibles.</span><span class="sxs-lookup"><span data-stu-id="dbb4e-153">Scaling will not work if you have used all hello cores available.</span></span> <span data-ttu-id="dbb4e-154">Par exemple, si vous avez une limite de 100 cœurs, cela signifie que vous pouvez avoir 100 instances de machine virtuelle A1 pour votre service cloud ou 50 instances de machine virtuelle A2.</span><span class="sxs-lookup"><span data-stu-id="dbb4e-154">For example, if you have a limit of 100 cores, this means you could have 100 A1 sized virtual machine instances for your cloud service, or 50 A2 sized virtual machine instances.</span></span>

## <a name="networking"></a><span data-ttu-id="dbb4e-155">Mise en réseau</span><span class="sxs-lookup"><span data-stu-id="dbb4e-155">Networking</span></span>
### <a name="i-cant-reserve-an-ip-in-a-multi-vip-cloud-service"></a><span data-ttu-id="dbb4e-156">Impossible de réserver une adresse IP dans un service cloud à plusieurs adresses IP virtuelles</span><span class="sxs-lookup"><span data-stu-id="dbb4e-156">I can't reserve an IP in a multi-VIP cloud service</span></span>
<span data-ttu-id="dbb4e-157">Tout d’abord, assurez-vous que cette instance de machine virtuelle hello que vous essayez tooreserve hello IP est activée.</span><span class="sxs-lookup"><span data-stu-id="dbb4e-157">First, make sure that hello virtual machine instance that you're trying tooreserve hello IP for is turned on.</span></span> <span data-ttu-id="dbb4e-158">En second lieu, assurez-vous que vous utilisez des adresses IP réservées pour les déploiements sembleront hello intermédiaire et de production.</span><span class="sxs-lookup"><span data-stu-id="dbb4e-158">Second, make sure that you're using Reserved IPs for bother hello staging and production deployments.</span></span> <span data-ttu-id="dbb4e-159">**Ne le faites pas** modifier les paramètres de hello pendant le déploiement de hello est mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="dbb4e-159">**Do not** change hello settings while hello deployment is upgrading.</span></span>

## <a name="remote-desktop"></a><span data-ttu-id="dbb4e-160">Bureau à distance</span><span class="sxs-lookup"><span data-stu-id="dbb4e-160">Remote desktop</span></span>
### <a name="how-do-i-remote-desktop-when-i-have-an-nsg"></a><span data-ttu-id="dbb4e-161">Comment établir un Bureau à distance lorsque je possède un groupe de sécurité réseau ?</span><span class="sxs-lookup"><span data-stu-id="dbb4e-161">How do I remote desktop when I have an NSG?</span></span>
<span data-ttu-id="dbb4e-162">Ajouter des règles toohello groupe de sécurité réseau qui autorisent le trafic sur les ports **3389** et **20000**.</span><span class="sxs-lookup"><span data-stu-id="dbb4e-162">Add rules toohello NSG that allow traffic on ports **3389** and **20000**.</span></span>  <span data-ttu-id="dbb4e-163">Bureau à distance utilise le port **3389**.</span><span class="sxs-lookup"><span data-stu-id="dbb4e-163">Remote Desktop uses port **3389**.</span></span>  <span data-ttu-id="dbb4e-164">Les instances de Service cloud sont à charge équilibrée, donc vous ne pouvez pas contrôler directement le tooconnect d’instance pour.</span><span class="sxs-lookup"><span data-stu-id="dbb4e-164">Cloud Service instances are load balanced, so you can't directly control which instance tooconnect to.</span></span>  <span data-ttu-id="dbb4e-165">Hello *RemoteForwarder* et *RemoteAccess* agents gérer le trafic RDP et hello client toosend un cookie RDP et de spécifier un tooconnect instance individuelle pour.</span><span class="sxs-lookup"><span data-stu-id="dbb4e-165">hello *RemoteForwarder* and *RemoteAccess* agents manage RDP traffic and allow hello client toosend an RDP cookie and specify an individual instance tooconnect to.</span></span>  <span data-ttu-id="dbb4e-166">Hello *RemoteForwarder* et *RemoteAccess* agents nécessitent ce port **20000*** être ouvert, ce qui peut être bloqué si vous disposez d’un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="dbb4e-166">hello *RemoteForwarder* and *RemoteAccess* agents require that port **20000*** be opened, which may be blocked if you have an NSG.</span></span>
