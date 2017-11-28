---
title: "Connexion de machines virtuelles SQL à Recherche Azure | Microsoft Docs"
description: "Activer les connexions chiffrées et configurer le pare-feu pour autoriser les connexions à SQL Server sur une machine virtuelle Azure à partir d’un indexeur sur Azure Search."
services: search
documentationcenter: 
author: HeidiSteen
manager: pablocas
editor: 
ms.assetid: 46e42e0e-c8de-4fec-b11a-ed132db7e7bc
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/23/2017
ms.author: heidist
ms.openlocfilehash: bb61330ba5511955e0da16dcd5b8b19529d0e44b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="configure-a-connection-from-an-azure-search-indexer-to-sql-server-on-an-azure-vm"></a>Configurer une connexion à partir d’un indexeur Azure Search à SQL Server sur une machine virtuelle Azure
Comme indiqué dans [Connexion d’Azure SQL Database à Recherche Azure à l’aide d’indexeurs](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md#faq), la création d’indexeurs dans **SQL Server sur des machines virtuelles Azure** (ou des **machines virtuelles SQL Azure** pour faire plus court) est prise en charge par le service Recherche Azure, mais il existe quelques conditions préalables liées à la sécurité qu’il faut résoudre en premier lieu. 

**Durée de la tâche :** environ 30 minutes, en supposant que vous avez déjà installé un certificat sur la machine virtuelle.

## <a name="enable-encrypted-connections"></a>Activer des connexions chiffrées
Le service Recherche Azure requiert un canal chiffré pour toutes les demandes d’indexeur via une connexion internet publique. Cette section répertorie les étapes pour y parvenir.

1. Vérifiez les propriétés du certificat pour vous assurer que le nom du sujet est le nom de domaine complet (FQDN) de la machine virtuelle Azure. Vous pouvez utiliser un outil tel que CertUtils ou le composant logiciel enfichable Certificats pour afficher les propriétés. Vous pouvez obtenir le nom de domaine complet à partir de la section Essentials du panneau du service de la machine virtuelle dans le champ **Adresse IP publique/Étiquette du nom DNS** dans le [portail Azure](https://portal.azure.com/).
   
   * Pour les machines virtuelles créées en utilisant le modèle **Resource Manager** le plus récent, le nom de domaine complet est au format `<your-VM-name>.<region>.cloudapp.azure.com`. 
   * Pour les machines virtuelles plus anciennes créées comme machines virtuelles **Classic**, le nom de domaine complet est au format `<your-cloud-service-name.cloudapp.net>`. 
2. Configurez SQL Server de manière à utiliser le certificat à l’aide de l’Éditeur du Registre (regedit). 
   
    Bien que le Gestionnaire de Configuration SQL Server soit souvent utilisé pour cette tâche, vous ne pouvez pas l’utiliser pour ce scénario. Il ne trouve pas le certificat importé, car le nom de domaine complet de la machine virtuelle sur Azure ne correspond pas au nom de domaine complet tel que déterminé par la machine virtuelle (il identifie le domaine en tant qu’ordinateur local ou domaine du réseau auquel il est joint). Lorsque les noms ne correspondent pas, utilisez regedit pour spécifier le certificat.
   
   * Dans regedit, accédez à la clé de Registre suivante : `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\[MSSQL13.MSSQLSERVER]\MSSQLServer\SuperSocketNetLib\Certificate`.
     
     La partie `[MSSQL13.MSSQLSERVER]` varie en fonction du nom de version et de l’instance. 
   * Définissez la valeur de la clé de **Certificat** sur l’**empreinte numérique** du certificat SSL que vous avez importé sur la machine virtuelle.
     
     Il existe plusieurs manières d’obtenir l’empreinte numérique, certaines étant mieux que d’autres. Si vous la copiez à partir du composant logiciel enfichable **certificats** dans MMC, vous allez probablement choisir un caractère de début invisible [comme décrit dans cet article du support technique](https://support.microsoft.com/kb/2023869/), ce qui entraîne une erreur lors de la tentative de connexion. Il existe plusieurs solutions de contournement pour résoudre ce problème. La plus simple consiste à reculer et retaper le premier caractère de l’empreinte numérique pour supprimer le caractère de début dans le champ de la valeur de clé dans regedit. Vous pouvez également utiliser un autre outil pour copier l’empreinte numérique.
3. Accordez des autorisations pour le compte de service. 
   
    Assurez-vous que le compte de service SQL Server a l’autorisation appropriée sur la clé privée du certificat SSL. Si vous ignorez cette étape, SQL Server ne démarre pas. Vous pouvez utiliser le composant logiciel enfichable **Certificats** ou **CertUtils** pour cette tâche.
4. Redémarrez le service SQL Server.

## <a name="configure-sql-server-connectivity-in-the-vm"></a>Configurer la connectivité SQL Server dans la machine virtuelle
Après avoir configuré la connexion chiffrée requise par Azure Search, vous devez réaliser des étapes de configuration supplémentaires intrinsèques à SQL Server sur les machines virtuelles Azure. Si vous ne l’avez pas déjà fait, l’étape suivante consiste à terminer la configuration en utilisant l’un de ces articles :

* Pour une machine virtuelle **Resource Manager** , consultez l’article [Connect to a SQL Server Virtual Machine on Azure using Resource Manager](../virtual-machines/windows/sql/virtual-machines-windows-sql-connect.md)(Se connecter à une machine virtuelle SQL Server sur Azure à l’aide de Resource Manager). 
* Pour une machine virtuelle **classique** , consultez [Connexion à une machine virtuelle sur Azure Classic](../virtual-machines/windows/classic/sql-connect.md).

En particulier, examinez la section de chaque article pour la « connexion via internet ».

## <a name="configure-the-network-security-group-nsg"></a>Configurer le groupe de sécurité réseau
Il n’est pas inhabituel de configurer le groupe de sécurité réseau et le point de terminaison correspondant ou la liste de contrôle d’accès Azure correspondant(e) pour rendre votre machine virtuelle Azure accessible à d’autres parties. Vous avez sans doute déjà effectué cela pour permettre à votre propre logique d’application de se connecter à votre machine virtuelle SQL Azure. C’est la même chose pour une connexion d’Azure Search à votre machine virtuelle SQL Azure. 

Les liens ci-dessous fournissent des instructions sur la configuration du groupe de sécurité réseau pour les déploiements de machines virtuelles. Utilisez ces instructions pour faire figurer un point de terminaison Azure SEarch dans la liste de contrôle d’accès en fonction de son adresse IP.

> [!NOTE]
> Pour obtenir des informations générales, consultez [Présentation du groupe de sécurité réseau](../virtual-network/virtual-networks-nsg.md)
> 
> 

* Pour une machine virtuelle **Resource Manager** , consultez [How to create NSGs for ARM deployments](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)(Procédure de création des groupes de sécurité réseau pour les déploiements ARM). 
* Pour une machine virtuelle **classique** , consultez [How to create NSGs for Classic deployments](../virtual-network/virtual-networks-create-nsg-classic-ps.md)(Procédure de création des groupes de sécurité réseau pour les déploiements classiques).

L’adressage IP peut poser quelques problèmes qui sont facilement surmontés si vous êtes conscient du problème et des solutions de contournement possibles. Les sections restantes fournissent des recommandations pour la gestion des problèmes liés aux adresses IP dans la liste de contrôle d’accès.

#### <a name="restrict-access-to-the-search-service-ip-address"></a>Restreindre l’accès à l’adresse IP du service de recherche
Nous vous recommandons fortement de restreindre l’accès à l’adresse IP de votre service de recherche dans la liste de contrôle d’accès au lieu de rendre vos machines virtuelles SQL Azure disponibles pour toutes les demandes de connexion. Vous pouvez facilement trouver l’adresse IP en exécutant une commande ping sur le nom de domaine complet (par exemple, `<your-search-service-name>.search.windows.net`) de votre service de recherche.

#### <a name="managing-ip-address-fluctuations"></a>Gestion des fluctuations d’adresse IP
Si votre service de recherche n’a qu’une seule unité de recherche (autrement dit, un réplica et une partition), l’adresse IP change lors d’un redémarrage du service de routine, ce qui invalide une liste de contrôle d’accès existante avec votre adresse IP du service de recherche.

Pour éviter l’erreur de connectivité qui s’ensuit, utilisez plusieurs réplicas et une partition dans Azure Search. Cela augmente le coût, mais permet également de résoudre le problème d’adresse IP. Dans Azure Search, les adresses IP ne changent pas lorsque vous avez plusieurs unités de recherche.

Une deuxième approche consiste à autoriser l’échec de la connexion et de reconfigurer les listes de contrôle d’accès dans le groupe de sécurité réseau. En moyenne, vous pouvez vous attendre à ce que les adresses IP soient modifiées à quelques semaines d’intervalle. Pour les clients qui procèdent à une indexation contrôlée de manière irrégulière, cette approche peut être viable.

Une troisième approche viable (mais pas particulièrement sécurisée) consiste à spécifier la plage d’adresses IP de la région Azure où votre service de recherche est configuré. La liste des plages d’adresses IP à partir desquelles les adresses IP publiques sont allouées à des ressources Azure est publiée dans [Plages d’adresses IP du centre de données Azure](https://www.microsoft.com/download/details.aspx?id=41653). 

#### <a name="include-the-azure-search-portal-ip-addresses"></a>Inclure les adresses IP du portail Azure Search
Si vous utilisez le portail Azure pour créer un indexeur, la logique du portail Azure Search doit également pouvoir accéder à votre machine virtuelle SQL Azure lors de la création. Exécutez la commande ping sur `stamp2.search.ext.azure.com`pour trouver les adresses IP du portail Azure Search.

## <a name="next-steps"></a>Étapes suivantes
Une fois la configuration résolue, vous pouvez maintenant spécifier un serveur SQL Server sur une machine virtuelle Azure comme source de données pour un indexeur Azure Search. Pour plus d’informations, consultez [Connexion d’Azure SQL Database à Azure Search à l’aide d’indexeurs](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md) .

