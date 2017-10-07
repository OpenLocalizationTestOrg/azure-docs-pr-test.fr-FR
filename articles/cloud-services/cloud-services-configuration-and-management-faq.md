---
title: "problèmes de gestion et d’aaaConfiguration pour le FAQ de Microsoft Azure Cloud Services | Documents Microsoft"
description: "Cet article répertorie les hello Forum aux questions sur la configuration et de gestion pour les Services de Cloud de Microsoft Azure."
services: cloud-services
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 62ece142ac0ef5d45081cab333375b1a0a8f0ab7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configuration-and-management-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a>Problèmes de configuration et de gestion pour Azure Cloud Services : questions fréquentes (FAQ)

Cet article comprend des questions fréquentes sur les problèmes de configuration et de gestion pour [Microsoft Azure Cloud Services](https://azure.microsoft.com/services/cloud-services). Vous pouvez également consulter hello [page de taille de machine virtuelle de Services Cloud](cloud-services-sizes-specs.md) pour les informations de taille.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="how-do-i-add-nosniff-toomy-website"></a>Comment ajouter le site Web de toomy « nosniff » ?
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

## <a name="how-do-i-customize-iis-for-a-web-role"></a>Comment personnaliser IIS pour un rôle web ?
Utiliser le script de démarrage IIS hello de hello [tâches courantes de démarrage](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) l’article.

## <a name="i-cannot-scale-beyond-x-instances"></a>Je ne parviens pas à mettre à l’échelle au-delà de X instances
Votre abonnement Azure a une limite de nombre de hello de cœurs que vous pouvez utiliser. Mise à l’échelle ne fonctionnera pas si vous avez utilisé tous les cœurs hello disponibles. Par exemple, si vous avez une limite de 100 cœurs, cela signifie que vous pouvez avoir 100 instances de machine virtuelle A1 pour votre service cloud ou 50 instances de machine virtuelle A2.

## <a name="how-can-i-implement-role-based-access-for-cloud-services"></a>Comment implémenter un accès en fonction du rôle pour les services cloud ?
Services de cloud computing ne prend en charge le modèle de contrôle d’accès en fonction du rôle (RBAC) hello, car il n’est pas un service Gestionnaire de ressources Azure en fonction.

Consultez [Comparaison entre RBAC Azure et les administrateur d’abonnements classiques](../active-directory/role-based-access-control-what-is.md#azure-rbac-vs-classic-subscription-administrators).

## <a name="how-do-i-set-hello-idle-timeout-for-azure-load-balancer"></a>Comment définir le délai d’inactivité de hello pour l’équilibrage de charge Azure ?
Vous pouvez spécifier le délai d’attente hello dans votre fichier de définition (csdef) de service comme suit :

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceDefinition name="mgVS2015Worker" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition" schemaVersion="2015-04.2.6">
  <WorkerRole name="WorkerRole1" vmsize="Small">
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" />
    </ConfigurationSettings>
    <Imports>
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
    <Endpoints>
      <InputEndpoint name="Endpoint1" protocol="tcp" port="10100"   idleTimeoutInMinutes="30" />
    </Endpoints>
  </WorkerRole>
```
Pour plus d’informations, consultez [Nouveau : délai d’inactivité configurable pour Azure Load Balancer](https://azure.microsoft.com/blog/new-configurable-idle-timeout-for-azure-load-balancer/).

## <a name="can-microsoft-internal-engineers-rdp-toocloud-service-instances-without-permission"></a>Peut les ingénieurs de Microsoft internes des instances de service de toocloud RDP sans autorisation ?
Suit Microsoft un processus strict n’autorisera pas interne ingénieurs tooRDP dans votre service cloud sans autorisation écrite (par courrier électronique ou toute autre communication écrite) propriétaire de hello ou leur représentant.

## <a name="why-is-hello-certificate-chain-of-my-cloud-service-ssl-certificate-incomplete"></a>Pourquoi la chaîne de certificats hello de mon certificat SSL du service cloud est incomplète ?
Nous recommandons aux clients d’installer chaîne de certificats complète hello (certificat de la feuille, les certificats intermédiaires et certificat racine) au lieu de simplement le certificat de feuille hello. Lorsque vous installez uniquement le certificat de feuille hello, vous fier à la chaîne de certificats Windows toobuild hello en parcourant hello CTL. En cas problèmes réseau intermittent ou DNS dans Azure ou de mise à jour Windows lorsque Windows tente de certificat de hello toovalidate, certificat de hello peut être considéré comme non valide. En installant la chaîne de certificats complète hello, ce problème peut être évité. Hello blog à [comment tooinstall un certificat SSL chaîné](https://blogs.msdn.microsoft.com/azuredevsupport/2010/02/24/how-to-install-a-chained-ssl-certificate/) montre comment toodo cela.

## <a name="how-do-i-associate-a-static-ip-address-toomy-cloud-service"></a>Comment pour associer un service de cloud des toomy d’adresses IP statique ?
tooset une adresse IP statique, vous devez toocreate une adresse IP réservée. Cette adresse IP réservée peut être associé tooa nouveau cloud service ou tooan déploiement existant. Hello suivant des documents pour plus d’informations, consultez :
* [Comment toocreate une adresse IP réservée](../virtual-network/virtual-networks-reserved-public-ip.md#manage-reserved-vips)
* [Réserver l’adresse IP de hello d’un service cloud existant](../virtual-network/virtual-networks-reserved-public-ip.md#reserve-the-ip-address-of-an-existing-cloud-service)
* [Associer un réservée IP tooa nouveau service cloud](../virtual-network/virtual-networks-reserved-public-ip.md#associate-a-reserved-ip-to-a-new-cloud-service)
* [Associer un tooa IP réservée déploiement en cours d’exécution](../virtual-network/virtual-networks-reserved-public-ip.md#associate-a-reserved-ip-to-a-running-deployment)
* [Associer un service de cloud tooa IP réservé à l’aide d’un fichier de configuration de service](../virtual-network/virtual-networks-reserved-public-ip.md#associate-a-reserved-ip-to-a-cloud-service-by-using-a-service-configuration-file)

## <a name="what-is-hello-quota-limit-for-my-cloud-service"></a>Quelle est la limite de quota hello pour mon service cloud ?
Consultez [Limites spécifiques des services](../azure-subscription-service-limits.md#subscription-limits).

## <a name="why-does-hello-drive-on-my-cloud-service-vm-show-very-little-free-disk-space"></a>Pourquoi le lecteur hello sur mon ordinateur virtuel de service cloud affiche-t-il très peu d’espace disque libre ?
Ce comportement est attendu, et il ne doit pas provoquer de n’importe quelle application tooyour de problème. La journalisation est activée pour hello % uproot lecteur dans les machines virtuelles Azure PaaS, qui consomme essentiellement de double hello quantité d’espace qui occupent généralement de fichiers. Cependant, il existe plusieurs choses toobe des essentiellement en faites pas un problème.

taille du lecteur % % approot Hello est calculée sous la forme < taille de fichier .cspkg + taille maximale de journal > + une marge d’espace libre, ou 1,5 Go, selon ce qui est plus grand. taille de Hello de votre machine virtuelle n’a aucune incidence sur ce calcul. (hello taille de machine virtuelle affecte uniquement taille hello du lecteur C: temporaire de hello). 

Il est le lecteur % approot non pris en charge toowrite toohello %. Si vous écrivez toohello machine virtuelle Azure, vous devez le faire dans une ressource LocalStorage temporaire (ou une autre option, tels que le stockage Blob, les fichiers Azure, etc..). Par conséquent, la quantité hello d’espace libre sur le dossier approot hello % n’est pas significative. Si vous n’êtes pas sûr si votre application écrit toohello approot lecteur, vous pouvez toujours laisser votre service s’exécutent pendant quelques jours et ensuite comparer hello « avant » et « après » tailles. 

Azure ne sera pas rien écrire toohello approot lecteur. Une fois hello disque dur virtuel est créé à partir de votre fichier .cspkg et monté dans hello Azure VM, seul hello peut écrire toothis lecteur est votre application. 

paramètres du journal Hello étant non configurable, vous ne pouvez pas le désactiver.

## <a name="what-are-hello-features-and-capabilities-that-azure-basic-ipsids-and-ddos-provides"></a>Quelles sont les fonctions hello et fonctionnalités qui fournit des adresses IP/ID de base Azure et DDOS ?
Azure a des adresses IP/ID dans toodefend de serveurs physiques de centre de données contre les menaces. Par ailleurs, les clients peuvent déployer des solutions de sécurité tierces, telles que des pare-feu d’applications web, des pare-feu réseau, des logiciels anti-programmes malveillants, des systèmes de détection et de prévention des intrusions (IDS/IPS), etc. Pour plus d’informations, consultez [Protégez vos données et vos biens en respectant les normes internationales de sécurité](https://www.microsoft.com/en-us/trustcenter/Security/AzureSecurity).

Microsoft surveille en permanence les menaces toodetect serveurs, réseaux et applications. L’approche multifronts menace pour la gestion de Azure utilise la détection d’intrusion, distribuée par déni de service (distribué DDoS) attaques prévention des tests d’intrusion, comportementales analytique, la détection d’anomalies et apprentissage tooconstantly renforcer sa protection et réduire les risques. Microsoft Antimalware pour Azure protège les services cloud et les machines virtuelles Azure. Vous avez hello option toodeploy tiers des solutions de sécurité en outre, tels que des murs d’incendie web application, pare-feu de réseau, logiciel anti-programme malveillant, détection et la prévention des intrusions (intrusion) et bien plus encore.

## <a name="why-does-iis-stop-writing-toohello-log-directory"></a>Pourquoi IIS arrête l’écriture du répertoire du journal toohello ?
Quota de stockage local hello pour l’écriture du répertoire du journal toohello avoir épuisé. Pour corriger ce problème, vous avez trois solutions :
* Activer les diagnostics pour IIS et avez hello diagnostics régulièrement déplacées tooblob stockage.
* Supprimez manuellement les fichiers journaux de hello répertoire de journalisation.
* Augmentez la limite de quota pour les ressources locales.

Pour plus d’informations, consultez hello suivant des documents :
* [Stocker et afficher des données de diagnostic dans le stockage Azure](cloud-services-dotnet-diagnostics-storage.md)
* [Le service Journaux IIS cesse d’écrire dans le service cloud](https://blogs.msdn.microsoft.com/cie/2013/12/21/iis-logs-stops-writing-in-cloud-service/)

## <a name="what-is-hello-purpose-of-hello-windows-azure-tools-encryption-certificate-for-extensions"></a>À quoi sert hello Hello « Windows Azure Tools chiffrement pour les Extensions de certificat » ?
Ces certificats sont automatiquement créés chaque fois qu’une extension est ajoutée toohello le service cloud. En règle générale, il s’agit hello extension des diagnostics Windows AZURE ou hello extension du protocole RDP, mais il peut s’agir d’autres personnes, par exemple hello extension anti-programme malveillant ou Log Collector. Ces certificats sont utilisés uniquement pour chiffrer et déchiffrer la configuration privée d’hello pour l’extension de hello. date d’expiration de Hello n’est jamais vérifiée, peu importe si hello certificat a expiré. 

Vous pouvez ignorer ces certificats. Si vous souhaitez nettoyer les certificats de hello, essayez de supprimer toutes les. Azure génère une erreur si vous essayez de toodelete un certificat qui est en cours d’utilisation.

## <a name="how-can-i-generate-a-certificate-signing-request-csr-without-rdp-ing-in-toohello-instance"></a>Comment puis-je générer un certificat de demande (signature) sans « RDP effectue une opération » dans l’instance de toohello ?
Consultez hello suivant Guide :

>[Obtention d’un certificat pour une utilisation avec Windows Azure Web Sites (WAWS)](https://azure.microsoft.com/blog/obtaining-a-certificate-for-use-with-windows-azure-web-sites-waws/)

Notez qu’une demande de signature de certificat consiste simplement en un fichier texte. Il n’a pas toobe créé à partir de l’ordinateur de hello où hello certificat sera finalement être utilisé. Bien que ce document est destiné à un Service d’application, hello la création de signature de certificat est générique et s’applique également pour les Services Cloud.
