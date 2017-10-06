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
# <a name="cloud-services-faq"></a>Forum aux questions sur les services cloud
Cet article répond à certaines questions fréquemment posées sur les services cloud Microsoft Azure. Vous pouvez aussi visiter hello [Forum aux questions sur Azure prend en charge](http://go.microsoft.com/fwlink/?LinkID=185083) pour plus d’informations de tarification et la prise en charge Azure. Vous pouvez également consulter hello [page de taille de machine virtuelle de Services Cloud](cloud-services-sizes-specs.md) pour les informations de taille.

## <a name="certificates"></a>Certificats
### <a name="where-should-i-install-my-certificate"></a>Où dois-je installer mon certificat ?
* **My**  
  Certificat d’application avec clé privée (\*.pfx, \*.p12).
* **CA**  
  Tous vos certificats intermédiaires sont stockés dans ce magasin (stratégie et autorités de certification secondaires).
* **ROOT**  
  magasin d’autorité de certification racine de Hello, afin de votre certificat d’autorité de certification racine principal doit être ici.

### <a name="i-cant-remove-expired-certificate"></a>Impossible de supprimer les certificats expirés
Azure vous empêche de supprimer un certificat s’il est en cours d’utilisation. Vous devez tooeither delete hello déploiement qui utilise le certificat de hello ou mise à jour hello déploiement avec un certificat différent ou renouvelé.

### <a name="delete-an-expired-certificate"></a>Suppression d’un certificat ayant expiré
Tant que certificat de hello n’est pas en cours d’utilisation, vous pouvez utiliser hello [Remove-AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) tooremove d’applet de commande PowerShell un certificat.

### <a name="i-have-expired-certificates-named-windows-azure-service-management-for-extensions"></a>Mes certificats Windows Azure Service Management for Extensions ont expiré
Ces certificats sont créés chaque fois qu’une extension est ajoutée le service de cloud computing toohello tels que hello extension du Bureau à distance. Ces certificats sont utilisés uniquement pour chiffrer et déchiffrer la configuration privée d’extension de hello d’hello. L’expiration de ces certificats n’a aucune importance. date d’expiration de Hello n’est pas vérifiée.

### <a name="certificates-i-have-deleted-keep-reappearing"></a>Les certificats que j’ai supprimés continuent à s’afficher
Ces certificats continuent de s’afficher en raison d’un outil que vous utilisez, comme Visual Studio. Chaque fois que vous vous reconnectez à un outil qui utilise un certificat, il sera à nouveau téléchargé tooAzure.

### <a name="my-certificates-keep-disappearing"></a>Mes certificats ne cessent de disparaître
Lorsque l’instance de machine virtuelle hello est recyclé, toutes les modifications locales sont perdues. Utilisez un [tâche de démarrage](cloud-services-startup-tasks.md) tooinstall certificats toohello virtual machine chaque heure hello démarre.

### <a name="i-cannot-find-my-management-certificates-in-hello-portal"></a>Impossible de trouver les certificats de gestion dans le portail de hello
[Certificats de gestion](../azure-api-management-certs.md) sont disponibles uniquement dans hello portail classique Azure. portail Azure actuel de Hello n’utilise pas de certificats de gestion. 

### <a name="how-can-i-disable-a-management-certificate"></a>Comment puis-je désactiver un certificat de gestion ?
[certificats de gestion](../azure-api-management-certs.md) ne peuvent pas être désactivés. Vous supprimer via hello portail classique Azure lorsque vous ne souhaitez pas que les toobe plus utilisé.

### <a name="how-do-i-create-an-ssl-certificate-for-a-specific-ip-address"></a>Comment créer un certificat SSL pour une adresse IP spécifique ?
Suivez les instructions de hello Bonjour [créer un didacticiel de certificat](cloud-services-certs-create.md). Utiliser l’adresse IP de hello comme hello nom DNS.

## <a name="security"></a>Sécurité
### <a name="disable-ssl-30"></a>Désactiver SSL 3.0
toodisable SSL 3.0 et TLS utilise la sécurité, créez une tâche de démarrage qui est décrit dans ce billet de blog : https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/

### <a name="add-nosniff-tooyour-website"></a>Ajouter **nosniff** tooyour site
les clients tooprevent à partir de la détection des types MIME de hello, ajoutez un paramètre dans votre *web.config* fichier.

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

Vous pouvez également ajouter ce paramètre dans IIS. Suivant de hello d’utilisation de commandes avec hello [tâches courantes de démarrage](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) l’article.

```cmd
%windir%\system32\inetsrv\appcmd set config /section:httpProtocol /+customHeaders.[name='X-Content-Type-Options',value='nosniff']
```

### <a name="customize-iis-for-a-web-role"></a>Personnaliser IIS pour un rôle web
Utiliser le script de démarrage IIS hello de hello [tâches courantes de démarrage](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) l’article.

## <a name="scaling"></a>Mise à l'échelle
### <a name="i-cannot-scale-beyond-x-instances"></a>Je ne parviens pas à mettre à l’échelle au-delà de X instances
Votre abonnement Azure a une limite de nombre de hello de cœurs que vous pouvez utiliser. Mise à l’échelle ne fonctionnera pas si vous avez utilisé tous les cœurs hello disponibles. Par exemple, si vous avez une limite de 100 cœurs, cela signifie que vous pouvez avoir 100 instances de machine virtuelle A1 pour votre service cloud ou 50 instances de machine virtuelle A2.

## <a name="networking"></a>Mise en réseau
### <a name="i-cant-reserve-an-ip-in-a-multi-vip-cloud-service"></a>Impossible de réserver une adresse IP dans un service cloud à plusieurs adresses IP virtuelles
Tout d’abord, assurez-vous que cette instance de machine virtuelle hello que vous essayez tooreserve hello IP est activée. En second lieu, assurez-vous que vous utilisez des adresses IP réservées pour les déploiements sembleront hello intermédiaire et de production. **Ne le faites pas** modifier les paramètres de hello pendant le déploiement de hello est mise à niveau.

## <a name="remote-desktop"></a>Bureau à distance
### <a name="how-do-i-remote-desktop-when-i-have-an-nsg"></a>Comment établir un Bureau à distance lorsque je possède un groupe de sécurité réseau ?
Ajouter des règles toohello groupe de sécurité réseau qui autorisent le trafic sur les ports **3389** et **20000**.  Bureau à distance utilise le port **3389**.  Les instances de Service cloud sont à charge équilibrée, donc vous ne pouvez pas contrôler directement le tooconnect d’instance pour.  Hello *RemoteForwarder* et *RemoteAccess* agents gérer le trafic RDP et hello client toosend un cookie RDP et de spécifier un tooconnect instance individuelle pour.  Hello *RemoteForwarder* et *RemoteAccess* agents nécessitent ce port **20000*** être ouvert, ce qui peut être bloqué si vous disposez d’un groupe de sécurité réseau.
