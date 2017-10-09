---
title: tooAzure de connexion de machine virtuelle aaaSQL recherche | Documents Microsoft
description: "Activer les connexions chiffrées et configurer hello pare-feu tooallow connexions tooSQL Server sur une machine virtuelle (VM) Azure à partir d’un indexeur sur Azure Search."
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
ms.openlocfilehash: 1f0db8a2812b0a7d012e58bb873c4b2b29fa1338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-connection-from-an-azure-search-indexer-toosql-server-on-an-azure-vm"></a>Configurer une connexion à partir d’un tooSQL d’indexeur Azure Search Server sur une machine virtuelle Azure
Comme indiqué dans [tooAzure de connexion de base de données SQL Azure de recherche à l’aide des indexeurs](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md#faq), création d’indexeurs contre **SQL Server sur des machines virtuelles Azure** (ou **machines virtuelles de SQL Azure** pour la forme courte) est prise en charge par Azure Search, mais il existe quelques tootake liées à la sécurité des conditions préalables requises administration premier. 

**Durée de la tâche :** environ 30 minutes, en supposant que vous déjà installé un certificat sur hello machine virtuelle.

## <a name="enable-encrypted-connections"></a>Activer des connexions chiffrées
Le service Recherche Azure requiert un canal chiffré pour toutes les demandes d’indexeur via une connexion internet publique. Cette section répertorie hello étapes toomake ce travail.

1. Vérifiez les propriétés hello hello certificat tooverify hello nom du sujet est le nom de domaine complet (FQDN) hello Hello machine virtuelle Azure. Vous pouvez utiliser un outil comme CertUtils ou hello des propriétés de hello tooview du composant logiciel enfichable Certificats. Vous pouvez obtenir hello nom de domaine complet à partir Essentials section du panneau service hello VM hello **Public adresse IP/nom DNS étiquette** champ Bonjour [portail Azure](https://portal.azure.com/).
   
   * Pour les machines virtuelles créées à l’aide de la plus récente de hello **le Gestionnaire de ressources** modèle, hello nom de domaine complet sous la forme `<your-VM-name>.<region>.cloudapp.azure.com`. 
   * Pour les machines virtuelles plus anciennes créés comme un **classique** machine virtuelle, le nom de domaine complet sous la forme de hello `<your-cloud-service-name.cloudapp.net>`. 
2. Configurez SQL Server toouse hello certificat à l’aide de hello Éditeur du Registre (regedit). 
   
    Bien que le Gestionnaire de Configuration SQL Server soit souvent utilisé pour cette tâche, vous ne pouvez pas l’utiliser pour ce scénario. Elle ne trouvera pas hello le certificat importé car hello nom de domaine complet de hello sur Azure ne correspond pas hello nom de domaine complet comme déterminé par hello VM (il identifie les domaine hello comme ordinateur local de hello ou toowhich de domaine réseau hello qu'il est joint). Lorsque les noms ne correspondent pas, utilisez le certificat de regedit toospecify hello.
   
   * Dans regedit, accédez à clé de Registre toothis : `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\[MSSQL13.MSSQLSERVER]\MSSQLServer\SuperSocketNetLib\Certificate`.
     
     Hello `[MSSQL13.MSSQLSERVER]` partie varie en fonction de la version nom et instance. 
   * La valeur hello Hello **certificat** toohello clé **l’empreinte numérique** du certificat SSL de hello vous avez importé toohello machine virtuelle.
     
     Il existe plusieurs façons tooget hello l’empreinte numérique, certains mieux que d’autres. Si vous le copiez à partir de hello **certificats** enfichable dans MMC, vous probablement prennent en charge un caractère de début invisible [comme décrit dans cet article de la prise en charge](https://support.microsoft.com/kb/2023869/), ce qui entraîne une erreur lorsque vous essayez d’un connexion. Il existe plusieurs solutions de contournement pour résoudre ce problème. Hello plus simple est toobackspace sur et retapez hello premier caractère de hello empreinte tooremove hello caractère de début dans le champ de valeur de clé hello dans regedit. Vous pouvez également utiliser une empreinte de hello toocopy autre outil.
3. Accorder les autorisations de compte de service de toohello. 
   
    Vérifiez que hello compte de service SQL Server est accordée l’autorisation appropriée sur la clé privée de hello du certificat SSL de hello. Si vous ignorez cette étape, SQL Server ne démarre pas. Vous pouvez utiliser hello **certificats** enfichable ou **CertUtils** pour cette tâche.
4. Redémarrez le service SQL Server de hello.

## <a name="configure-sql-server-connectivity-in-hello-vm"></a>Configurer la connectivité SQL Server Bonjour machine virtuelle
Après avoir configuré la connexion hello chiffré requise par la recherche Azure, il existe une configuration supplémentaire étapes tooSQL intrinsèque Server sur des machines virtuelles Azure. Si vous n’avez pas déjà fait, étape suivante de hello est configuration toofinish à l’aide de l’une de ces articles :

* Pour un **le Gestionnaire de ressources** machine virtuelle, consultez [connecter tooa Machine virtuelle de SQL Server sur Azure à l’aide du Gestionnaire de ressources](../virtual-machines/windows/sql/virtual-machines-windows-sql-connect.md). 
* Pour un **classique** machine virtuelle, consultez [connecter tooa Machine virtuelle de SQL Server sur Azure Classic](../virtual-machines/windows/classic/sql-connect.md).

Vérifiez en particulier la section hello dans chaque article pour « qui se connectent via hello d’internet ».

## <a name="configure-hello-network-security-group-nsg"></a>Configurer le groupe de sécurité réseau (NSG) de hello
Il n’est pas rare tooconfigure hello NSG et point de terminaison Azure correspondant ou liste de contrôle d’accès (ACL) toomake vos parties tooother accessible de machine virtuelle Azure. Sans doute que vous avez effectuée cela tooallow votre propre tooyour de tooconnect application logique SQL Azure VM. Il n’est pas différente d’un tooyour de connexion SQL Azure VM Azure Search. 

liens Hello ci-dessous fournissent des instructions sur la configuration de groupe de sécurité réseau pour les déploiements d’ordinateurs virtuels. Utilisez ces instructions que tooacl un point de terminaison Azure SEarch en fonction de son adresse IP.

> [!NOTE]
> Pour obtenir des informations générales, consultez [Présentation du groupe de sécurité réseau](../virtual-network/virtual-networks-nsg.md)
> 
> 

* Pour un **le Gestionnaire de ressources** machine virtuelle, consultez [comment toocreate groupes de sécurité réseau pour les déploiements de ARM](../virtual-network/virtual-networks-create-nsg-arm-pportal.md). 
* Pour un **classique** machine virtuelle, consultez [comment toocreate groupes de sécurité réseau pour les déploiements standard](../virtual-network/virtual-networks-create-nsg-classic-ps.md).

Adressage IP peut présenter quelques défis auxquels sont résoudre facilement si vous êtes conscient des problème de hello et des solutions de contournement. les sections restantes Hello fournissent des recommandations pour la gestion des problèmes connexes tooIP adresses hello ACL.

#### <a name="restrict-access-toohello-search-service-ip-address"></a>Restreindre l’adresse IP du service de recherche des accès toohello
Nous vous recommandons vivement de limiter hello toohello IP adresse de votre service de recherche Bonjour ACL au lieu d’effectuer vos machines virtuelles de SQL Azure large ouvrir tooany les demandes de connexion. Vous pouvez facilement trouver des hello IP adresse par la commande ping hello nom de domaine complet (par exemple, `<your-search-service-name>.search.windows.net`) de votre service de recherche.

#### <a name="managing-ip-address-fluctuations"></a>Gestion des fluctuations d’adresse IP
Si votre service de recherche n'a qu’une seule unité de recherche (autrement dit, un réplica et une partition), adresse IP de hello change lors d’un redémarrage du service de la routine, invalider une ACL existante avec l’adresse IP de votre service recherche.

Erreur de connectivité suivants tooavoid monodirectionnelle hello est toouse plus d’un réplica et une partition dans Azure Search. Cela augmente les coûts de hello, mais qu’il résout également problème d’adressage IP hello. Dans Azure Search, les adresses IP ne changent pas lorsque vous avez plusieurs unités de recherche.

Une deuxième approche est tooallow hello connexion toofail, puis reconfigurez hello ACL Bonjour groupe de sécurité réseau. En moyenne, vous pouvez vous attendre toochange d’adresses IP toutes les semaines. Pour les clients qui procèdent à une indexation contrôlée de manière irrégulière, cette approche peut être viable.

Une troisième approche viable (mais pas particulièrement sécurisée) est la plage d’adresses IP toospecify hello Hello région Azure où votre service de recherche est fourni. Hello la liste des plages d’adresses IP à partir de laquelle les adresses IP publiques tooAzure les ressources sont allouées est publiée à [plages d’adresses IP du centre de données Azure](https://www.microsoft.com/download/details.aspx?id=41653). 

#### <a name="include-hello-azure-search-portal-ip-addresses"></a>Inclure les adresses IP portails hello Azure Search
Si vous utilisez hello toocreate portail Azure un indexeur, une logique de portail Azure Search doit également accès tooyour SQL Azure VM lors de la création. Exécutez la commande ping sur `stamp2.search.ext.azure.com`pour trouver les adresses IP du portail Azure Search.

## <a name="next-steps"></a>Étapes suivantes
Avec la configuration de la façon de hello, vous pouvez maintenant spécifier un serveur SQL Server sur machine virtuelle Azure en tant que source de données hello pour un indexeur Azure Search. Consultez [tooAzure de connexion de base de données SQL Azure de recherche à l’aide des indexeurs](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md) pour plus d’informations.

