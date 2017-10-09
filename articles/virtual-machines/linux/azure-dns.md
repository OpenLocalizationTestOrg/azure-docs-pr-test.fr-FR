---
title: "aaaDNS options de résolution de noms pour les ordinateurs virtuels Linux dans Azure"
description: "Scénarios de résolution de noms pour les machines virtuelles Linux dans Azure IaaS, notamment les services DNS fournis, le DNS externe hybride et l’apport de son propre serveur DNS."
services: virtual-machines
documentationcenter: na
author: RicksterCDN
manager: timlt
editor: tysonn
ms.assetid: 787a1e04-cebf-4122-a1b4-1fcf0a2bbf5f
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/19/2016
ms.author: rclaus
ms.openlocfilehash: 7df2320b6f6b42b479bf4070ea60fe5770a78a41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="dns-name-resolution-options-for-linux-virtual-machines-in-azure"></a>Options de résolution de noms DNS pour les machines virtuelles Linux dans Azure
Azure fournit une résolution des noms DNS par défaut pour toutes les machines virtuelles d’un même réseau virtuel. Vous pouvez implémenter votre propre solution de résolution de noms DNS en configurant vos propres services DNS sur vos machines virtuelles hébergées sur Azure. Hello scénarios suivants vous aideront à choisir hello qui fonctionne pour votre situation.

* [Résolution de noms fournie par Azure](#azure-provided-name-resolution)
* [Résolution de noms à l’aide de votre propre serveur DNS](#name-resolution-using-your-own-dns-server)

type Hello de résolution de noms que vous utilisez dépend du mode vos machines virtuelles et les instances de rôle doivent toocommunicate entre eux.

Hello tableau suivant illustre des scénarios et solutions de résolution de nom correspondantes :

| **Scénario** | **Solution** | **Suffixe** |
| --- | --- | --- |
| Résolution de noms entre instances de rôle ou machines virtuelles dans hello même réseau virtuel |[Résolution de noms fournie par Azure](#azure-provided-name-resolution) |nom d’hôte ou nom de domaine complet |
| Résolution de noms entre des instances de rôle ou des machines virtuelles situées dans des réseaux virtuels différents |Serveurs DNS gérés par le client qui transfèrent les requêtes entre les réseaux virtuels pour une résolution par Azure (proxy DNS). Consultez [Résolution de noms à l’aide de votre propre serveur DNS](#name-resolution-using-your-own-dns-server). |Nom de domaine complet uniquement |
| Résolution des noms de service et d’ordinateur locaux à partir des instances de rôle ou des machines virtuelles dans Azure |Serveurs DNS gérés par le client (par exemple contrôleur de domaine local, contrôleur de domaine en lecture seule local ou serveur DNS secondaire synchronisé via des transferts de zone). Consultez [Résolution de noms à l’aide de votre propre serveur DNS](#name-resolution-using-your-own-dns-server). |Nom de domaine complet uniquement |
| Résolution de noms d’hôte Azure à partir d’ordinateurs locaux |Transférer les requêtes tooa gérée par le client DNS serveur proxy dans le réseau virtuel correspondant de hello. serveur de proxy Hello transfère tooAzure de requêtes pour la résolution. Consultez [Résolution de noms à l’aide de votre propre serveur DNS](#name-resolution-using-your-own-dns-server). |Nom de domaine complet uniquement |
| DNS inversé pour les adresses IP internes |[Résolution de noms à l’aide de votre propre serveur DNS](#name-resolution-using-your-own-dns-server) |n/a |

## <a name="name-resolution-that-azure-provides"></a>Résolution de noms fournie par Azure
Avec la résolution de noms DNS publics, Azure fournit la résolution de noms interne pour les machines virtuelles et instances de rôle qui se trouvent dans hello même réseau virtuel. Dans les réseaux virtuels basés sur le Gestionnaire de ressources Azure, hello suffixe DNS n’est cohérente sur le réseau virtuel de hello. nom de domaine complet de Hello n’est pas nécessaire. Les noms DNS peuvent être affectées tooboth cartes d’interface réseau (NIC) et les machines virtuelles. Bien que la résolution de noms hello fournis par Azure ne nécessite pas de configuration, il n’est pas hello le choix approprié pour tous les scénarios de déploiement, comme l’illustre le tableau précédent de hello.

### <a name="features-and-considerations"></a>Fonctionnalités et considérations
**Fonctionnalités :**

* Aucune configuration n’est la résolution de noms toouse requis par Microsoft Azure.
* service de résolution de noms Hello fournis par Azure est hautement disponible. Vous ne devez toocreate et gérer des clusters de vos propres serveurs DNS.
* service de résolution de noms Hello fournis par Azure peut être utilisé avec vos propres tooresolve de serveurs DNS locaux et les noms d’hôte Azure.
* Résolution de noms est fournie entre les machines virtuelles dans des réseaux virtuels sans avoir besoin de hello nom de domaine complet.
* Vous pouvez utiliser des noms d’hôtes qui décrivent vos déploiements de façon plus appropriée, au lieu de noms générés automatiquement.

**Considérations :**

* suffixe DNS Hello qu’Azure crée ne peut pas être modifié.
* Vous ne pouvez pas enregistrer manuellement vos propres enregistrements.
* WINS et NetBIOS ne sont pas pris en charge.
* Les noms d’hôte doivent être compatibles avec DNS.
    Les noms doivent comporter uniquement les caractères 0-9, a-z et « - », et ils ne peuvent pas commencer ou se terminer par « - ». Consultez RFC 3696 Section 2.
* Le trafic des requêtes DNS est limité pour chaque machine virtuelle. Cette limitation ne devrait pas avoir d’incidence sur la plupart des applications.  Si la limitation de requêtes est respectée, assurez-vous que la mise en cache côté client est activée.  Pour plus d’informations, consultez [obtention de la plupart à partir de la résolution de noms fournis par Azure hello](#getting-the-most-from-name-resolution-that-azure-provides).

### <a name="getting-hello-most-from-name-resolution-that-azure-provides"></a>Obtention de la plupart à partir de la résolution de noms fournis par Azure hello
**Mise en cache côté client :**

Certaines requêtes DNS ne sont pas envoyées réseau hello. La mise en cache côté client permet de réduire la latence et améliorer des incohérences de résilience toonetwork en résolvant les requêtes DNS récurrentes d’un cache local. Enregistrements DNS contiennent une durée de vie (TTL), qui permet l’enregistrement de hello toostore hello cache aussi longtemps que possible sans affecter l’actualisation d’enregistrement. Pour cette raison, la mise en cache côté client convient donc à la plupart des situations.

Certaines distributions Linux n’incluent pas la mise en cache par défaut. Nous vous recommandons une machine virtuelle de cache tooeach Linux après avoir vérifié qu’il n’est pas un cache local déjà.

Plusieurs packages de mise en cache DNS sont disponibles, comme dnsmasq. Voici hello étapes tooinstall dnsmasq sur les distributions de courants hello :

**Ubuntu (utilise resolvconf)**
  * Installer hello dnsmasq (« sudo apt-get install dnsmasq »).

**SUSE (utilise netconf)**:
1. Installer hello dnsmasq (« sudo zypper installation dnsmasq »).
2. Activer le service de dnsmasq hello (« systemctl activer dnsmasq.service »).
3. Démarrer le service de dnsmasq hello (« systemctl début dnsmasq.service »).
4. Modifier « / etc/sysconfig/réseau/config » et modifiez NETCONFIG_DNS_FORWARDER = » « trop « dnsmasq ».
5. Mettre à jour resolv.conf (« netconfig mise à jour ») tooset hello cache comme hello du programme de résolution DNS local.

**CentOS de Rogue Wave Software (anciennement OpenLogic, utilise NetworkManager)**
1. Installer hello dnsmasq (« sudo yum installation dnsmasq »).
2. Activer le service de dnsmasq hello (« systemctl activer dnsmasq.service »).
3. Démarrer le service de dnsmasq hello (« systemctl début dnsmasq.service »).
4. Ajoutez « ajouter des serveurs de nom de domaine 127.0.0.1 ; » too"/etc/dhclient-eth0.conf ».
5. Redémarrez du cache (« service réseau restart ») tooset hello hello network service hello du programme de résolution DNS local

> [!NOTE]
> : hello 'dnsmasq' package doit uniquement de hello nombreux DNS met en cache qui sont disponibles pour Linux. Avant de l’utiliser, vérifiez son adéquation à vos besoins et qu’aucun autre cache n’est installé.
>
>

**Nouvelles tentatives côté client**

DNS est principalement un protocole UDP. Hello protocole UDP ne garantissent la remise des messages, hello protocole DNS lui-même gère la logique de nouvelle tentative. Chaque client DNS (système d’exploitation) peut présenter la logique de nouvelle tentative différents selon les préférences du créateur hello :

* Les systèmes d’exploitation Windows effectuent une nouvelle tentative après une seconde, puis à nouveau après deux secondes, quatre secondes et encore quatre secondes.
* Bonjour nouvelles tentatives d’installation de Linux par défaut après cinq secondes.  Vous devez modifier cette tooretry cinq fois à intervalles d’une seconde.  

toocheck hello paramètres actuels sur une machine virtuelle Linux, « cat /etc/resolv.conf » et rechercher en ligne de 'options' hello, par exemple :

    options timeout:1 attempts:5

fichier de resolv.conf Hello est généré automatiquement et ne doit pas être modifié. Hello des étapes spécifiques qui ajouter hello 'options' ligne varient selon la distribution :

**Ubuntu** (utilise resolvconf)
1. Ajouter hello options ligne too'/etc/resolveconf/resolv.conf.d/head'.
2. Exécutez 'resolvconf -u' tooupdate.

**SUSE** (utilise netconf)
1. Ajoutez 'timeout:1 tentatives : 5' toohello NETCONFIG_DNS_RESOLVER_OPTIONS = » « paramètre de '/ etc/sysconfig/réseau/config'.
2. Exécutez 'netconfig update' tooupdate.

**CentOS de Rogue Wave Software (anciennement OpenLogic)** (utilise NetworkManager)
1. Ajoutez « echo « options timeout:1 tentatives : 5 « » de too'/etc/NetworkManager/dispatcher.d/11-dhclient'.
2. Exécutez « redémarrage du service réseau » tooupdate.

## <a name="name-resolution-using-your-own-dns-server"></a>Résolution de noms à l’aide de votre propre serveur DNS
Vos besoins de résolution de nom peuvent aller au-delà des fonctionnalités de hello fournis par Azure. Par exemple, vous pouvez avoir besoin d’une résolution DNS entre des réseaux virtuels. toocover ce scénario, vous pouvez utiliser vos propres serveurs DNS.  

Les serveurs DNS dans un peuvent réseau virtuel vers l’avant DNS interroge toorecursive des programmes de résolution de noms d’hôtes tooresolve Azure qui se trouvent dans hello même réseau virtuel. Par exemple, un serveur DNS qui s’exécute dans Azure peut répondre requêtes tooDNS pour son propre serveur DNS de la zone fichiers et transférer toutes les autres tooAzure de requêtes. Cette fonctionnalité permet des deux entrées dans vos fichiers de zone et les noms d’hôtes fournis par Azure (via le redirecteur de hello) de votre toosee de machines virtuelles. Programmes de résolution de l’accès toohello récursive de Azure est fournie via l’adresse IP virtuelle hello 168.63.129.16.

Le transfert DNS également permet la résolution DNS entre les réseaux virtuels et votre nom d’hôte du tooresolve de machines sur site Azure fournit. tooresolve nom d’hôte de l’ordinateur virtuel, hello DNS du serveur virtuel doivent résider dans hello même réseau virtuel et être tooAzure de requêtes de nom d’hôte tooforward configuré. Étant donné que le suffixe DNS de hello est différent dans chaque réseau virtuel, vous pouvez utiliser le transfert conditionnel règles toosend DNS interroge toohello corriger un réseau virtuel pour la résolution. Hello image suivante montre deux réseaux virtuels et un réseau local effectuant la résolution DNS entre les réseaux virtuels à l’aide de cette méthode :

![Résolution DNS entre réseaux virtuels](./media/azure-dns/inter-vnet-dns.png)

Lorsque vous utilisez la résolution de noms fournis par Azure, les suffixes DNS interne hello sont fourni tooeach virtuels à l’aide de DHCP. Lorsque vous utilisez votre propre solution de résolution de nom, ce suffixe n’est pas fourni toovirtual machines, car le suffixe de hello interfère avec d’autres architectures DNS. toomachines toorefer par nom de domaine complet ou tooconfigure suffixe hello sur vos ordinateurs virtuels, vous pouvez utiliser PowerShell ou hello du suffixe de hello API toodetermine :

* Pour les réseaux virtuels qui sont gérés par le Gestionnaire de ressources Azure, le suffixe de hello est disponible via hello [carte d’interface réseau](https://msdn.microsoft.com/library/azure/mt163668.aspx) ressource. Vous pouvez également exécuter hello `azure network public-ip show <resource group> <pip name>` commande Détails de hello toodisplay de votre adresse IP publique, qui inclut hello nom de domaine complet de hello carte réseau.

Si la redirection des requêtes tooAzure ne suffit pas, vous devez tooprovide votre propre solution DNS.  Votre solution DNS doit :

* Fournir la résolution de nom d’hôte approprié, par exemple par le biais de [DDNS](../../virtual-network/virtual-networks-name-resolution-ddns.md). Si vous utilisez DDNS, vous devrez peut-être le nettoyage des enregistrements DNS toodisable. Les baux DHCP d’Azure sont très longs et le nettoyage peut supprimer prématurément des enregistrements DNS.
* Fournissent une résolution tooallow récursive appropriée la résolution de noms de domaines externes.
* Être accessible (TCP et UDP sur le port 53) à partir de clients hello fait et être en mesure de tooaccess hello Internet.
* Être protégé contre tout accès à partir de hello Internet toomitigate les menaces posées par les agents externes.

> [!NOTE]
> Pour de meilleures performances, lorsque vous utilisez des machines virtuelles sur des serveurs DNS de Azure, désactiver IPv6 et affecter un [IP publiques au niveau de l’Instance](../../virtual-network/virtual-networks-instance-level-public-ip.md) tooeach DNS du serveur virtuel.  
>
>
