---
title: "FAQ sur les rôles Services cloud Azure | Microsoft Docs"
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
ms.openlocfilehash: d887f3b31693c414254dc01dac4dbdd6d9224b6d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="cloud-services-faq"></a><span data-ttu-id="5e475-104">Forum aux questions sur les services cloud</span><span class="sxs-lookup"><span data-stu-id="5e475-104">Cloud Services FAQ</span></span>
<span data-ttu-id="5e475-105">Cet article répond à certaines questions fréquemment posées sur les services cloud Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="5e475-105">This article answers some frequently asked questions about Microsoft Azure Cloud Services.</span></span> <span data-ttu-id="5e475-106">Vous pouvez également visiter le [FAQ du support Azure](http://go.microsoft.com/fwlink/?LinkID=185083) pour obtenir des informations de support et de tarification générale Azure.</span><span class="sxs-lookup"><span data-stu-id="5e475-106">You can also visit the [Azure Support FAQ](http://go.microsoft.com/fwlink/?LinkID=185083) for general Azure pricing and support information.</span></span> <span data-ttu-id="5e475-107">Vous pouvez également consulter la page [Taille de services cloud](cloud-services-sizes-specs.md) pour obtenir des informations sur la taille.</span><span class="sxs-lookup"><span data-stu-id="5e475-107">You can also consult the [Cloud Services VM Size page](cloud-services-sizes-specs.md) for size information.</span></span>

## <a name="certificates"></a><span data-ttu-id="5e475-108">Certificats</span><span class="sxs-lookup"><span data-stu-id="5e475-108">Certificates</span></span>
### <a name="where-should-i-install-my-certificate"></a><span data-ttu-id="5e475-109">Où dois-je installer mon certificat ?</span><span class="sxs-lookup"><span data-stu-id="5e475-109">Where should I install my certificate?</span></span>
* <span data-ttu-id="5e475-110">**My**</span><span class="sxs-lookup"><span data-stu-id="5e475-110">**My**</span></span>  
  <span data-ttu-id="5e475-111">Certificat d’application avec clé privée (\*.pfx, \*.p12).</span><span class="sxs-lookup"><span data-stu-id="5e475-111">Application Certificate with private key (\*.pfx, \*.p12).</span></span>
* <span data-ttu-id="5e475-112">**CA**</span><span class="sxs-lookup"><span data-stu-id="5e475-112">**CA**</span></span>  
  <span data-ttu-id="5e475-113">Tous vos certificats intermédiaires sont stockés dans ce magasin (stratégie et autorités de certification secondaires).</span><span class="sxs-lookup"><span data-stu-id="5e475-113">All your intermediate certificates go in this store (Policy and Sub CAs).</span></span>
* <span data-ttu-id="5e475-114">**ROOT**</span><span class="sxs-lookup"><span data-stu-id="5e475-114">**ROOT**</span></span>  
  <span data-ttu-id="5e475-115">Magasin de l’autorité de certification racine (par conséquent, il s’agit de l’emplacement de votre certificat principal de l’autorité de certification racine.</span><span class="sxs-lookup"><span data-stu-id="5e475-115">The root CA store, so your main root CA cert should go here.</span></span>

### <a name="i-cant-remove-expired-certificate"></a><span data-ttu-id="5e475-116">Impossible de supprimer les certificats expirés</span><span class="sxs-lookup"><span data-stu-id="5e475-116">I can't remove expired certificate</span></span>
<span data-ttu-id="5e475-117">Azure vous empêche de supprimer un certificat s’il est en cours d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="5e475-117">Azure prevents you from removing a certificate while it is in use.</span></span> <span data-ttu-id="5e475-118">Vous devez soit supprimer le déploiement qui utilise le certificat, soit mettre à jour le déploiement avec un autre certificat ou avec un certificat que vous avez renouvelé.</span><span class="sxs-lookup"><span data-stu-id="5e475-118">You need to either delete the deployment that uses the certificate, or update the deployment with a different or renewed certificate.</span></span>

### <a name="delete-an-expired-certificate"></a><span data-ttu-id="5e475-119">Suppression d’un certificat ayant expiré</span><span class="sxs-lookup"><span data-stu-id="5e475-119">Delete an expired certificate</span></span>
<span data-ttu-id="5e475-120">Vous pouvez utiliser l’applet de commande PowerShell [Remove-AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) pour supprimer un certificat, à condition qu’il n’est pas utilisé.</span><span class="sxs-lookup"><span data-stu-id="5e475-120">As long as the certificate is not in use, you can use the [Remove-AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) PowerShell cmdlet to remove a certificate.</span></span>

### <a name="i-have-expired-certificates-named-windows-azure-service-management-for-extensions"></a><span data-ttu-id="5e475-121">Mes certificats Windows Azure Service Management for Extensions ont expiré</span><span class="sxs-lookup"><span data-stu-id="5e475-121">I have expired certificates named Windows Azure Service Management for Extensions</span></span>
<span data-ttu-id="5e475-122">Ces certificats sont créés chaque fois qu’une extension, par exemple l’extension du Bureau à distance, est ajoutée au service cloud.</span><span class="sxs-lookup"><span data-stu-id="5e475-122">These certificates are created whenever an extension is added to the cloud service such as the Remote Desktop extension.</span></span> <span data-ttu-id="5e475-123">Ces certificats sont utilisés uniquement pour le chiffrement et le déchiffrement de la configuration privée de l’extension.</span><span class="sxs-lookup"><span data-stu-id="5e475-123">These certificates are only used for encrypting and decrypting the private configuration of the extension.</span></span> <span data-ttu-id="5e475-124">L’expiration de ces certificats n’a aucune importance.</span><span class="sxs-lookup"><span data-stu-id="5e475-124">It does not matter if these certificates expire.</span></span> <span data-ttu-id="5e475-125">La date d’expiration n’est pas vérifiée.</span><span class="sxs-lookup"><span data-stu-id="5e475-125">The expiration date is not checked.</span></span>

### <a name="certificates-i-have-deleted-keep-reappearing"></a><span data-ttu-id="5e475-126">Les certificats que j’ai supprimés continuent à s’afficher</span><span class="sxs-lookup"><span data-stu-id="5e475-126">Certificates I have deleted keep reappearing</span></span>
<span data-ttu-id="5e475-127">Ces certificats continuent de s’afficher en raison d’un outil que vous utilisez, comme Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5e475-127">These keep reappearing most likely because of a tool you're using, such as Visual Studio.</span></span> <span data-ttu-id="5e475-128">À chaque fois que vous vous reconnectez avec un outil qui utilise un certificat, il sera à nouveau téléchargé dans Azure.</span><span class="sxs-lookup"><span data-stu-id="5e475-128">Whenever you reconnect with a tool that is using a certificate, it will again be uploaded to Azure.</span></span>

### <a name="my-certificates-keep-disappearing"></a><span data-ttu-id="5e475-129">Mes certificats ne cessent de disparaître</span><span class="sxs-lookup"><span data-stu-id="5e475-129">My certificates keep disappearing</span></span>
<span data-ttu-id="5e475-130">Chaque nouveau cycle de l’instance de machine virtuelle entraîne la perte de toutes les modifications locales.</span><span class="sxs-lookup"><span data-stu-id="5e475-130">When the virtual machine instance recycles, all local changes are lost.</span></span> <span data-ttu-id="5e475-131">Utilisez une [tâche de démarrage](cloud-services-startup-tasks.md) pour installer les certificats sur la machine virtuelle à chaque démarrage du rôle.</span><span class="sxs-lookup"><span data-stu-id="5e475-131">Use a [startup task](cloud-services-startup-tasks.md) to install certificates to the virtual machine each time the role starts.</span></span>

### <a name="i-cannot-find-my-management-certificates-in-the-portal"></a><span data-ttu-id="5e475-132">Impossible de trouver les certificats de gestion dans le portail</span><span class="sxs-lookup"><span data-stu-id="5e475-132">I cannot find my management certificates in the portal</span></span>
<span data-ttu-id="5e475-133">Les [certificats de gestion](../azure-api-management-certs.md) sont uniquement disponibles dans le portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="5e475-133">[Management certificates](../azure-api-management-certs.md) are only available in the Azure Classic Portal.</span></span> <span data-ttu-id="5e475-134">Le portail Azure actuel n’utilise pas de certificats de gestion.</span><span class="sxs-lookup"><span data-stu-id="5e475-134">The current Azure portal does not use management certificates.</span></span> 

### <a name="how-can-i-disable-a-management-certificate"></a><span data-ttu-id="5e475-135">Comment puis-je désactiver un certificat de gestion ?</span><span class="sxs-lookup"><span data-stu-id="5e475-135">How can I disable a management certificate?</span></span>
<span data-ttu-id="5e475-136">[certificats de gestion](../azure-api-management-certs.md) ne peuvent pas être désactivés.</span><span class="sxs-lookup"><span data-stu-id="5e475-136">[Management certificates](../azure-api-management-certs.md) cannot be disabled.</span></span> <span data-ttu-id="5e475-137">Vous les supprimez via le portail Azure Classic lorsque vous ne souhaitez plus les utiliser.</span><span class="sxs-lookup"><span data-stu-id="5e475-137">You delete them through the Azure Classic Portal when you do not want them to be used anymore.</span></span>

### <a name="how-do-i-create-an-ssl-certificate-for-a-specific-ip-address"></a><span data-ttu-id="5e475-138">Comment créer un certificat SSL pour une adresse IP spécifique ?</span><span class="sxs-lookup"><span data-stu-id="5e475-138">How do I create an SSL certificate for a specific IP address?</span></span>
<span data-ttu-id="5e475-139">Suivez les instructions du [didacticiel de création de certificat](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="5e475-139">Follow the directions in the [create a certificate tutorial](cloud-services-certs-create.md).</span></span> <span data-ttu-id="5e475-140">Utilisez l’adresse IP en tant que nom DNS.</span><span class="sxs-lookup"><span data-stu-id="5e475-140">Use the IP address as the DNS Name.</span></span>

## <a name="security"></a><span data-ttu-id="5e475-141">Sécurité</span><span class="sxs-lookup"><span data-stu-id="5e475-141">Security</span></span>
### <a name="disable-ssl-30"></a><span data-ttu-id="5e475-142">Désactiver SSL 3.0</span><span class="sxs-lookup"><span data-stu-id="5e475-142">Disable SSL 3.0</span></span>
<span data-ttu-id="5e475-143">Pour désactiver SSL 3.0 et utiliser la sécurité TLS, créez une tâche de démarrage qui est décrite dans ce billet de blog : https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/</span><span class="sxs-lookup"><span data-stu-id="5e475-143">To disable SSL 3.0 and use TLS security, create a startup task which is documented on this blog post: https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/</span></span>

### <a name="add-nosniff-to-your-website"></a><span data-ttu-id="5e475-144">Ajouter **nosniff** à votre site web</span><span class="sxs-lookup"><span data-stu-id="5e475-144">Add **nosniff** to your website</span></span>
<span data-ttu-id="5e475-145">Pour empêcher les clients de détecter les types MIME, ajoutez un paramètre au fichier *web.config*.</span><span class="sxs-lookup"><span data-stu-id="5e475-145">To prevent clients from sniffing the MIME types, add a setting in your *web.config* file.</span></span>

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

<span data-ttu-id="5e475-146">Vous pouvez également ajouter ce paramètre dans IIS.</span><span class="sxs-lookup"><span data-stu-id="5e475-146">You can also add this as a setting in IIS.</span></span> <span data-ttu-id="5e475-147">Utilisez la commande suivante avec l’article [tâches courantes de démarrage](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe).</span><span class="sxs-lookup"><span data-stu-id="5e475-147">Use the following command with the [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) article.</span></span>

```cmd
%windir%\system32\inetsrv\appcmd set config /section:httpProtocol /+customHeaders.[name='X-Content-Type-Options',value='nosniff']
```

### <a name="customize-iis-for-a-web-role"></a><span data-ttu-id="5e475-148">Personnaliser IIS pour un rôle web</span><span class="sxs-lookup"><span data-stu-id="5e475-148">Customize IIS for a web role</span></span>
<span data-ttu-id="5e475-149">Utilisez le script de démarrage IIS à partir de l’article [tâches courantes de démarrage](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe).</span><span class="sxs-lookup"><span data-stu-id="5e475-149">Use the IIS startup script from the [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) article.</span></span>

## <a name="scaling"></a><span data-ttu-id="5e475-150">Mise à l'échelle</span><span class="sxs-lookup"><span data-stu-id="5e475-150">Scaling</span></span>
### <a name="i-cannot-scale-beyond-x-instances"></a><span data-ttu-id="5e475-151">Je ne parviens pas à mettre à l’échelle au-delà de X instances</span><span class="sxs-lookup"><span data-stu-id="5e475-151">I cannot scale beyond X instances</span></span>
<span data-ttu-id="5e475-152">Le nombre de cœurs que vous pouvez utiliser est limité dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="5e475-152">Your Azure Subscription has a limit on the number of cores you can use.</span></span> <span data-ttu-id="5e475-153">La mise à l’échelle ne fonctionnera pas si vous avez utilisé tous les cœurs disponibles.</span><span class="sxs-lookup"><span data-stu-id="5e475-153">Scaling will not work if you have used all the cores available.</span></span> <span data-ttu-id="5e475-154">Par exemple, si vous avez une limite de 100 cœurs, cela signifie que vous pouvez avoir 100 instances de machine virtuelle A1 pour votre service cloud ou 50 instances de machine virtuelle A2.</span><span class="sxs-lookup"><span data-stu-id="5e475-154">For example, if you have a limit of 100 cores, this means you could have 100 A1 sized virtual machine instances for your cloud service, or 50 A2 sized virtual machine instances.</span></span>

## <a name="networking"></a><span data-ttu-id="5e475-155">Mise en réseau</span><span class="sxs-lookup"><span data-stu-id="5e475-155">Networking</span></span>
### <a name="i-cant-reserve-an-ip-in-a-multi-vip-cloud-service"></a><span data-ttu-id="5e475-156">Impossible de réserver une adresse IP dans un service cloud à plusieurs adresses IP virtuelles</span><span class="sxs-lookup"><span data-stu-id="5e475-156">I can't reserve an IP in a multi-VIP cloud service</span></span>
<span data-ttu-id="5e475-157">Tout d’abord, vérifiez que l’instance de machine virtuelle pour laquelle vous tentez de réserver l’adresse IP est activée.</span><span class="sxs-lookup"><span data-stu-id="5e475-157">First, make sure that the virtual machine instance that you're trying to reserve the IP for is turned on.</span></span> <span data-ttu-id="5e475-158">Ensuite, assurez-vous que vous utilisez des adresses IP réservées aussi bien pour les déploiements intermédiaires que pour les déploiements de production.</span><span class="sxs-lookup"><span data-stu-id="5e475-158">Second, make sure that you're using Reserved IPs for bother the staging and production deployments.</span></span> <span data-ttu-id="5e475-159">**Ne** modifiez pas les paramètres pendant la mise à niveau du déploiement.</span><span class="sxs-lookup"><span data-stu-id="5e475-159">**Do not** change the settings while the deployment is upgrading.</span></span>

## <a name="remote-desktop"></a><span data-ttu-id="5e475-160">Bureau à distance</span><span class="sxs-lookup"><span data-stu-id="5e475-160">Remote desktop</span></span>
### <a name="how-do-i-remote-desktop-when-i-have-an-nsg"></a><span data-ttu-id="5e475-161">Comment établir un Bureau à distance lorsque je possède un groupe de sécurité réseau ?</span><span class="sxs-lookup"><span data-stu-id="5e475-161">How do I remote desktop when I have an NSG?</span></span>
<span data-ttu-id="5e475-162">Ajoutez des règles à un groupe de sécurité réseau qui autorisent le trafic sur les ports **3389** et **20000**.</span><span class="sxs-lookup"><span data-stu-id="5e475-162">Add rules to the NSG that allow traffic on ports **3389** and **20000**.</span></span>  <span data-ttu-id="5e475-163">Bureau à distance utilise le port **3389**.</span><span class="sxs-lookup"><span data-stu-id="5e475-163">Remote Desktop uses port **3389**.</span></span>  <span data-ttu-id="5e475-164">Les instances de service cloud sont soumis à l’équilibrage de charge, donc vous ne pouvez pas contrôler directement à quelle instance vous vous connectez.</span><span class="sxs-lookup"><span data-stu-id="5e475-164">Cloud Service instances are load balanced, so you can't directly control which instance to connect to.</span></span>  <span data-ttu-id="5e475-165">Les agents *RemoteForwarder* et *RemoteAccess* gèrent le trafic RDP, et permettent au client d’envoyer un cookie RDP et de spécifier une instance individuelle à laquelle se connecter.</span><span class="sxs-lookup"><span data-stu-id="5e475-165">The *RemoteForwarder* and *RemoteAccess* agents manage RDP traffic and allow the client to send an RDP cookie and specify an individual instance to connect to.</span></span>  <span data-ttu-id="5e475-166">Les agents *RemoteForwarder* et *RemoteAccess* nécessitent que ce port **20000*** soit ouvert : il peut être bloqué si vous avez un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="5e475-166">The *RemoteForwarder* and *RemoteAccess* agents require that port **20000*** be opened, which may be blocked if you have an NSG.</span></span>
