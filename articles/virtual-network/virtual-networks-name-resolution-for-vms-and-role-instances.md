---
title: "aaaResolution pour les machines virtuelles et Instances de rôle"
description: "Scénarios de résolution de noms pour Microsoft Azure IaaS, les solutions hybrides, entre différents services cloud, Active Directory et à l’aide de votre propre serveur DNS  "
services: virtual-network
documentationcenter: na
author: GarethBradshawMSFT
manager: carmonm
editor: tysonn
ms.assetid: 5d73edde-979a-470a-b28c-e103fcf07e3e
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/06/2016
ms.author: telmos
ms.openlocfilehash: 0ec7903cf200c1d04d75601a5b0cefe4268f3dcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="name-resolution-for-vms-and-role-instances"></a>Résolution de noms pour les machines virtuelles et les instances de rôle
Selon la façon dont vous utilisez toohost Azure IaaS, PaaS et des solutions hybrides, vous devrez peut-être tooallow hello machines virtuelles et instances de rôle que vous créez toocommunicate entre eux. Bien que cette communication peut être effectuée à l’aide d’adresses IP, il est beaucoup plus simples noms toouse faciles à retenir et ne changent pas. 

Lorsque les instances de rôle et des machines virtuelles hébergées dans Azure doivent les adresses IP toointernal tooresolve domaine noms, ils peuvent utiliser une des deux méthodes :

* [Résolution de noms dans Azure](#azure-provided-name-resolution)
* [Résolution de noms à l’aide de votre propre serveur DNS](#name-resolution-using-your-own-dns-server) (qui peut transmettre les requêtes toohello serveurs DNS fournis par Azure) 

type Hello de résolution de noms que vous utilisez dépend du mode vos machines virtuelles et les instances de rôle doivent toocommunicate entre eux.

**Hello tableau suivant illustre des scénarios et solutions de résolution de nom correspondantes :**

| **Scénario** | **Solution** | **Suffixe** |
| --- | --- | --- |
| Résolution de noms entre instances de rôle ou machines virtuelles situées dans hello même service cloud ou réseau virtuel |[Résolution de noms dans Azure](#azure-provided-name-resolution) |Nom d’hôte ou nom de domaine complet |
| Résolution de noms entre des instances de rôles ou des machines virtuelles situées dans différents réseaux virtuels |Serveurs DNS gérés par le client qui redirigent les requêtes entre les réseaux virtuels en vue de la résolution par Azure (proxy DNS).  Consultez [Résolution de noms à l’aide de votre propre serveur DNS](#name-resolution-using-your-own-dns-server) |Nom de domaine complet uniquement |
| Résolution des noms de service et d’ordinateur locaux à partir des instances de rôle ou des machines virtuelles dans Azure |Serveurs DNS gérés par le client (par exemple, contrôleur de domaine local, contrôleur de domaine en lecture seule local ou serveur DNS secondaire synchronisé à l’aide de transferts de zone).  See [Résolution de noms à l’aide de votre propre serveur DNS](#name-resolution-using-your-own-dns-server) |Nom de domaine complet uniquement |
| Résolution de noms d’hôte Azure à partir d’ordinateurs locaux |Transmettre les requêtes tooa gérée par le client DNS serveur proxy dans le réseau virtuel correspondant de hello, serveur de proxy hello transfère tooAzure de requêtes pour la résolution. See [Résolution de noms à l’aide de votre propre serveur DNS](#name-resolution-using-your-own-dns-server) |Nom de domaine complet uniquement |
| DNS inversé pour les adresses IP internes |[Résolution de noms à l’aide de votre propre serveur DNS](#name-resolution-using-your-own-dns-server) |n/a |
| Résolution de noms entre des machines virtuelles ou instances de rôle situées dans différents services cloud, non dans un réseau virtuel |Non applicable. La connectivité entre des machines virtuelles et des instances de rôle de différents services cloud n’est pas prise en charge en dehors d’un réseau virtuel. |n/a |

## <a name="azure-provided-name-resolution"></a>Résolution de noms dans Azure
Avec la résolution de noms DNS publics, Azure fournit la résolution de noms interne pour les machines virtuelles et instances de rôle qui résident dans hello même service cloud ou réseau virtuel.  Machines virtuelles/instances dans un service cloud partagent hello DNS mêmes suffixe (afin que le nom d’hôte de hello seul est suffisant), mais dans les services de cloud différents réseaux virtuels classiques peuvent avoir différents suffixes DNS hello nom de domaine complet est nécessaire tooresolve des noms entre différents services cloud.  Dans les réseaux virtuels dans le modèle de déploiement du Gestionnaire de ressources hello, suffixe DNS de hello est cohérent réseau virtuel hello (hello nom de domaine complet est donc pas nécessaire) et les noms DNS peuvent être affectés tooboth NIC et les machines virtuelles. Bien que la résolution de noms fournie par Azure ne nécessite aucune configuration, il n’est pas hello le choix approprié pour tous les scénarios de déploiement, comme indiqué sur la table hello ci-dessus.

> [!NOTE]
> Dans les cas de hello de rôles web et de travail, vous pouvez également accéder hello adresses IP internes des instances de rôle en fonction de hello rôle nom et numéro d’instance à l’aide de hello API REST gestion des services Azure. Pour plus d’informations, voir [Référence de l’API REST de gestion des services](https://msdn.microsoft.com/library/azure/ee460799.aspx).
> 
> 

### <a name="features-and-considerations"></a>Fonctionnalités et considérations
**Fonctionnalités :**

* Facilité d’utilisation : aucune configuration n’est requise dans l’ordre toouse résolution de noms fournie par Azure.
* service de résolution nom fourni par Azure de Hello est hautement disponible, l’enregistrement hello vous devez toocreate et gérer des clusters de vos propres serveurs DNS.
* Peut être utilisé conjointement avec votre propre tooresolve de serveurs DNS locaux et les noms d’hôte Azure.
* Résolution de noms est fournie entre les instances de rôle/VMs dans hello même service de cloud computing sans besoin d’un nom de domaine complet.
* Résolution de noms est fournie entre les machines virtuelles dans des réseaux virtuels qui utilisent le modèle de déploiement du Gestionnaire de ressources hello, sans avoir besoin de hello nom de domaine complet. Réseaux virtuels dans le modèle de déploiement classique hello nécessitent hello nom de domaine complet lors de la résolution de noms dans différents services cloud. 
* Vous pouvez utiliser des noms d’hôtes qui décrivent vos déploiements de manière plus appropriée, plutôt que des noms générés automatiquement.

**Considérations :**

* suffixe DNS créé par Azure Hello ne peut pas être modifié.
* Vous ne pouvez pas enregistrer manuellement vos propres enregistrements.
* WINS et NetBIOS ne sont pas pris en charge. (Vous ne pouvez pas voir vos machines virtuelles dans l’Explorateur Windows.)
* Les noms d’hôte doivent être compatibles DNS (ils doivent comporter uniquement les caractères 0-9, a-z et « - » et ne peuvent pas démarrer ou se terminer par un « - ». Voir la section 2 de RFC 3696.)
* Le trafic de requêtes DNS est limité pour chaque machine virtuelle. Cela ne devrait pas avoir d’incidence sur la plupart des applications.  Si la limitation de requêtes est respectée, assurez-vous que la mise en cache côté client est activée.  Pour plus d’informations, consultez [obtention de la plupart à partir de la résolution de noms fournie par Azure hello](#Getting-the-most-from-Azure-provided-name-resolution).
* Machines virtuelles uniquement hello 180 premiers services cloud sont inscrits pour chaque réseau virtuel dans un modèle de déploiement classique. Cela ne s’applique pas réseaux toovirtual dans les modèles de déploiement de gestionnaire de ressources.

### <a name="getting-hello-most-from-azure-provided-name-resolution"></a>Obtention de la plupart à partir de la résolution de noms fournie par Azure hello
**Mise en cache côté client :**

Pas toutes les requêtes DNS doit toobe envoyée sur le réseau de hello.  La mise en cache côté client permet de réduire la latence et améliorer blips toonetwork de résilience en résolvant les requêtes DNS récurrentes d’un cache local.  Enregistrements DNS contiennent une durée de vie (TTL) qui permet l’enregistrement de hello toostore hello cache aussi longtemps que possible sans affecter l’actualisation de l’enregistrement, par conséquent, la mise en cache côté client est appropriée pour la plupart des situations.

la valeur par défaut de Hello Client DNS de Windows a un cache DNS intégré.  Certains Linux versions n’incluent pas la mise en cache par défaut, il est recommandé qu’un ajoutés tooeach Linux VM (après vérification qu’il n’est pas un cache local déjà).

Il existe un nombre de différents DNS mise en cache packages disponibles, par exemple, dnsmasq, voici hello étapes tooinstall dnsmasq sur les versions principales hello :

* **Ubuntu (utilise resolvconf)**:
  * simplement hello dnsmasq package d’installation (« sudo apt-get install dnsmasq »).
* **SUSE (utilise netconf)**:
  * installer le package de dnsmasq hello (« sudo zypper installation dnsmasq ») 
  * Activer le service hello dnsmasq (« systemctl activer dnsmasq.service ») 
  * Démarrer le service de dnsmasq hello (« systemctl début dnsmasq.service ») 
  * modifier « / etc/sysconfig/réseau/config » et remplacez NETCONFIG_DNS_FORWARDER = » « trop « dnsmasq »
  * mettre à jour resolv.conf (« netconfig mise à jour ») tooset hello cache comme hello du programme de résolution DNS local
* **OpenLogic (utilise NetworkManager)**:
  * installer le package de dnsmasq hello (« sudo yum installation dnsmasq »)
  * Activer le service hello dnsmasq (« systemctl activer dnsmasq.service »)
  * Démarrer le service de dnsmasq hello (« systemctl début dnsmasq.service »)
  * Ajoutez « ajouter des serveurs de nom de domaine 127.0.0.1 ; » too"/etc/dhclient-eth0.conf »
  * Redémarrez du cache (« service réseau restart ») tooset hello hello network service hello du programme de résolution DNS local

> [!NOTE]
> package de « dnsmasq » Hello n’est qu’une Hello plusieurs caches DNS disponibles pour Linux.  Avant de l’utiliser, vérifiez son adéquation à vos besoins et assurez-vous qu’aucun autre cache n’est installé.
> 
> 

**Nouvelles tentatives côté client :**

DNS est principalement un protocole UDP.  Comme hello protocole UDP ne garantit la remise des messages, logique de nouvelle tentative est gérée dans le protocole hello de lui-même.  Chaque client DNS (système d’exploitation) peut présenter la logique de nouvelle tentative différents selon la préférence de créateurs hello :

* Les systèmes d’exploitation Windows effectuent de nouvelles tentatives après 1 seconde, puis à nouveau après 2 secondes, 4 secondes et encore 4 secondes. 
* Bonjour nouvelles tentatives d’installation de Linux par défaut après 5 secondes.  Il est recommandé de cette tooretry toochange 5 fois intervalles de 1 seconde.  

toocheck hello paramètres actuels sur un VM Linux, '/etc/resolv.conf cat' et ressembler à la ligne de 'options' hello, par exemple :

    options timeout:1 attempts:5

fichier de resolv.conf Hello est généralement générée automatiquement et ne doit pas être modifié.  des étapes spécifiques Hello pour ajouter la ligne hello 'options' varient selon le distributeur :

* **Ubuntu** (utilise resolvconf) :
  * Ajouter hello options ligne too'/etc/resolveconf/resolv.conf.d/head' 
  * Exécutez 'resolvconf -u' tooupdate
* **SUSE** (utilise netconf) :
  * Ajoutez 'timeout:1 tentatives : 5' toohello NETCONFIG_DNS_RESOLVER_OPTIONS = » « paramètre de '/ etc/sysconfig/réseau/config' 
  * Exécutez 'netconfig update' tooupdate
* **OpenLogic** (utilise NetworkManager) :
  * Ajoutez « echo « options timeout:1 tentatives : 5 « » de too'/etc/NetworkManager/dispatcher.d/11-dhclient' 
  * Exécutez « redémarrage du service réseau » tooupdate

## <a name="name-resolution-using-your-own-dns-server"></a>Résolution de noms à l’aide de votre propre serveur DNS
Il existe un certain nombre de situations où vos besoins de résolution de nom peuvent aller au-delà des fonctionnalités hello fournies par Azure, par exemple lorsque l’utilisation des domaines Active Directory, ou lorsque vous avez besoin de résolution DNS entre les réseaux virtuels (réseaux virtuels).  toocover ces scénarios, Azure permet hello vous toouse vos propres serveurs DNS.  

Les serveurs DNS dans un réseau virtuel peuvent transférer des programmes de résolution de tooAzure de requêtes DNS récursives tooresolve les noms d’hôtes au sein de ce réseau virtuel.  Par exemple, un contrôleur de domaine (DC) en cours d’exécution dans Azure peuvent répondre tooDNS de requêtes pour ses domaines et transférer toutes les autres tooAzure de requêtes.  Ainsi, les machines virtuelles toosee vos ressources locales (via hello contrôleur de domaine) et les noms d’hôte fourni par Azure (via le redirecteur de hello).  Programmes de résolution de tooAzure accès récursif est fournie via l’adresse IP virtuelle hello 168.63.129.16.

Le transfert de DNS Active la résolution DNS de réseau virtuel inter également et permet à votre tooresolve d’ordinateurs locaux des noms d’hôte fourni par Azure.  Dans commande tooresolve nom d’hôte de l’ordinateur virtuel, la machine virtuelle du serveur DNS hello doit se trouver dans hello même virtuel réseau et être tooAzure de requêtes de nom d’hôte tooforward configuré.  Comme suffixe DNS hello est différent dans chaque réseau virtuel, vous pouvez utiliser le transfert conditionnel règles toosend DNS interroge toohello corriger le réseau virtuel pour la résolution.  Hello suivant image montre deux réseaux virtuels et un réseau local effectuant la résolution DNS inter-réseau virtuel à l’aide de cette méthode.  Redirecteur DNS exemple est disponible dans hello [la galerie de modèles de démarrage rapide Azure](https://azure.microsoft.com/documentation/templates/301-dns-forwarder/) et [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/301-dns-forwarder).

![DNS entre réseaux virtuels](./media/virtual-networks-name-resolution-for-vms-and-role-instances/inter-vnet-dns.png)

Lorsque vous utilisez la résolution de noms fournie par Azure, un suffixe DNS interne (*. internal.cloudapp.net) est fourni tooeach machine virtuelle à l’aide de DHCP.  Cela permet la résolution de nom d’hôte en tant que nom d’hôte hello enregistrements figurant dans la zone de internal.cloudapp.net hello.  Lorsque vous utilisez votre propre solution de résolution de nom, hello suffixe de domaine internationaux n’est pas fourni tooVMs parce qu’il interfère avec d’autres architectures DNS (par exemple, les scénarios à un domaine).  Au lieu de cela, nous fournissons un espace réservé non fonctionnel (reddog.microsoft.com).  

Si nécessaire, suffixe DNS interne de hello peut être déterminé à l’aide de PowerShell ou hello API :

* Pour les réseaux virtuels dans les modèles de déploiement de gestionnaire de ressources, le suffixe de hello est disponible via hello [carte d’interface réseau](https://msdn.microsoft.com/library/azure/mt163668.aspx) ressource ou via hello [Get-AzureRmNetworkInterface](https://msdn.microsoft.com/library/mt619434.aspx) applet de commande.    
* Dans les modèles de déploiement classique, le suffixe de hello est disponible via hello [obtenir les API de déploiement](https://msdn.microsoft.com/library/azure/ee460804.aspx) appeler ou via hello [Get-AzureVM-déboguer](https://msdn.microsoft.com/library/azure/dn495236.aspx) applet de commande.

Si la redirection des requêtes tooAzure ne suffit pas, vous devez tooprovide votre propre solution DNS.  Votre solution DNS doit présenter les caractéristiques suivantes :

* Fournir la résolution de nom d’hôte approprié, par exemple par le biais de [DDNS](virtual-networks-name-resolution-ddns.md).  Notez que si des enregistrements à l’aide de DDNS, vous devrez peut-être toodisable DNS le nettoyage des enregistrements comme les baux DHCP de Azure sont très longs et le nettoyage peut supprimer DNS prématurément. 
* Fournissent une résolution tooallow récursive appropriée la résolution de noms de domaines externes.
* Être accessible (TCP et UDP sur le port 53) à partir de clients hello il sert et être en mesure de tooaccess hello internet.
* Être protégé contre tout accès à partir de hello internet, toomitigate les menaces posées par les agents externes.

> [!NOTE]
> Pour de meilleures performances, lors de l’utilisation de machines virtuelles Azure en tant que serveurs DNS, IPv6 doit être désactivée et un [IP publiques au niveau de l’Instance](virtual-networks-instance-level-public-ip.md) doivent être assignées tooeach machine virtuelle du serveur DNS.  Si vous choisissez toouse Windows Server en tant que votre serveur DNS, [cet article](http://blogs.technet.com/b/networking/archive/2015/08/19/name-resolution-performance-of-a-recursive-windows-dns-server-2012-r2.aspx) fournit une analyse des performances supplémentaires et des optimisations.
> 
> 

### <a name="specifying-dns-servers"></a>Spécification des serveurs DNS
Lorsque vous utilisez vos propres serveurs DNS, Azure fournit hello capacité toospecify plusieurs serveurs DNS par réseau virtuel ou par le réseau de l’interface (Resource Manager) / (classiques) de service cloud.  Serveurs DNS spécifiés pour une interface réseau/service de cloud obtiennent la priorité sur ceux spécifiés pour le réseau virtuel de hello.

> [!NOTE]
> Propriétés de connexion réseau, telles que le serveur DNS, des adresses IP ne doit pas être modifié directement dans les machines virtuelles Windows comme ils peuvent obtenir effacées pendant le service de correction lors de la carte réseau virtuelle de hello est remplacé. 
> 
> 

Lorsque vous utilisez le modèle de déploiement du Gestionnaire de ressources hello, les serveurs DNS peuvent être spécifiés dans hello Portal, API/modèles ([vnet](https://msdn.microsoft.com/library/azure/mt163661.aspx), [nic](https://msdn.microsoft.com/library/azure/mt163668.aspx)) ou de PowerShell ([réseau virtuel](https://msdn.microsoft.com/library/mt603657.aspx), [association](https://msdn.microsoft.com/library/mt619370.aspx)).

Lorsque vous utilisez le modèle de déploiement classique de hello, serveurs DNS pour le réseau virtuel de hello peut être spécifié dans hello portail ou [hello *Configuration réseau* fichier](https://msdn.microsoft.com/library/azure/jj157100).  Services de cloud computing, les serveurs DNS de hello sont spécifiées via [hello *Configuration du Service* fichier](https://msdn.microsoft.com/library/azure/ee758710) ou de PowerShell ([New-AzureVM](https://msdn.microsoft.com/library/azure/dn495254.aspx)).

> [!NOTE]
> Si vous modifiez les paramètres DNS de hello pour un ordinateur réseau/virtuel qui est déjà déployée, vous devez toorestart chaque machine virtuelle affecté pour effet de tootake modifications hello.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
Modèle de déploiement Resource Manager :

* [Création ou mise à jour d’un réseau virtuel](https://msdn.microsoft.com/library/azure/mt163661.aspx)
* [Création ou mise à jour d’une carte d’interface réseau](https://msdn.microsoft.com/library/azure/mt163668.aspx)
* [New-AzureRmVirtualNetwork](https://msdn.microsoft.com/library/mt603657.aspx)
* [New-AzureRmNetworkInterface](https://msdn.microsoft.com/library/mt619370.aspx)

Modèle de déploiement classique :

* [Schéma de configuration de service Microsoft Azure](https://msdn.microsoft.com/library/azure/ee758710)
* [Schéma de configuration du réseau virtuel](https://msdn.microsoft.com/library/azure/jj157100)
* [Configuration d'un réseau virtuel à l'aide d'un fichier de configuration réseau](virtual-networks-using-network-configuration-file.md) 

