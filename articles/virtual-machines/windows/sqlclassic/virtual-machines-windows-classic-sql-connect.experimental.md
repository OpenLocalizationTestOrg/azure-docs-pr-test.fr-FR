---
title: aaaConnect tooa Machine virtuelle de SQL Server sur Azure (classique) | Documents Microsoft
description: "Découvrez comment tooconnect tooSQL Server en cours d’exécution sur un ordinateur virtuel dans Azure. Cette rubrique utilise le modèle de déploiement classique hello. scénarios de Hello diffèrent en fonction de la configuration du réseau hello et l’emplacement de hello du client de hello."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-service-management
ms.assetid: 416948af-454f-4cfe-8fd2-7cf971cbd3e9
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/31/2017
ms.author: jroth
experimental_id: d51f3cc6-753b-4e
ms.openlocfilehash: 9577e4bdad79435e34a64fc669ec4848649fc945
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-sql-server-virtual-machine-on-azure-classic-deployment"></a>Se connecter tooa Machine virtuelle de SQL Server sur Azure (déploiement classique)
> [!div class="op_single_selector"]
> * [Gestionnaire de ressources](../sql/virtual-machines-windows-sql-connect.md)
> * [Classique](../classic/sql-connect.md)
> 
> 

## <a name="overview"></a>Vue d'ensemble
Cette rubrique décrit comment tooconnect tooyour SQL Server de l’instance en cours d’exécution sur une machine virtuelle Azure. Elle aborde certains [scénarios de connectivité générale](#connection-scenarios) et fournit une [procédure détaillée pour configurer la connectivité à SQL Server dans une machine virtuelle Azure](#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).

> [!IMPORTANT] 
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../azure-resource-manager/resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello. Si vous utilisez des machines virtuelles du Gestionnaire de ressources, consultez [connecter tooa Machine virtuelle de SQL Server sur Azure à l’aide du Gestionnaire de ressources](../sql/virtual-machines-windows-sql-connect.md).

## <a name="connection-scenarios"></a>Scénarios de connexion
moyen de Hello un client connecte tooSQL Server s’exécutant sur un ordinateur virtuel diffère selon l’emplacement de hello du client de hello et configuration de réseau/hello. Ces scénarios sont les suivants :

* [Se connecter tooSQL Server Bonjour même service cloud](#connect-to-sql-server-in-the-same-cloud-service)
* [Se connecter tooSQL Server sur hello internet](#connect-to-sql-server-over-the-internet)
* [Se connecter tooSQL Server Bonjour même réseau virtuel](#connect-to-sql-server-in-the-same-virtual-network)

> [!NOTE]
> Avant de vous connectez avec une de ces méthodes, vous devez suivre hello [les étapes de cette connexion de tooconfigure article](#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).
> 
> 

### <a name="connect-toosql-server-in-hello-same-cloud-service"></a>Se connecter tooSQL Server Bonjour même service cloud
Plusieurs ordinateurs virtuels peuvent être créés dans hello même service cloud. toounderstand ce virtual machines scénario, consultez [comment virtuels tooconnect avec un service cloud ou réseau virtuel](../classic/connect-vms.md#connect-vms-in-a-standalone-cloud-service). Dans ce scénario, un client sur une machine virtuelle tente tooconnect tooSQL serveur s’exécutant sur un autre ordinateur virtuel Bonjour même service cloud.

Dans ce scénario, vous pouvez vous connecter à l’aide de la machine virtuelle de hello **nom** (représentée par **nom de l’ordinateur** ou **nom d’hôte** dans le portail de hello). Il s’agit de nom hello que vous avez fourni pour hello machine virtuelle lors de la création. Par exemple, si vous avez nommé votre VM SQL **mysqlvm**, une machine virtuelle cliente Bonjour même service cloud peut utiliser hello suivant tooconnect de chaîne de connexion :

    "Server=mysqlvm;Integrated Security=false;User ID=<login_name>;Password=<your_password>"

### <a name="connect-toosql-server-over-hello-internet"></a>Se connecter tooSQL Server sur hello Internet
Si vous souhaitez que le moteur de base de données SQL Server tooconnect tooyour de hello Internet, vous devez créer un point de terminaison de machine virtuelle pour les communications TCP entrantes. Cette étape de configuration Azure dirige TCP port trafic tooa le port TCP entrant qui est accessible toohello virtual machine.

tooconnect sur hello internet, vous devez utiliser DNS hello et nom de machine virtuelle point de terminaison numéro de port la machine virtuelle hello (configuré plus loin dans cet article). toofind hello nom DNS, accédez toohello Azure portail, puis sélectionnez **machines virtuelles (classiques)**. Sélectionnez ensuite votre machine virtuelle. Hello **nom DNS** figure dans hello **vue d’ensemble** section.

Prenons par exemple une machine virtuelle classique nommée **mysqlvm** avec comme nom DNS **mysqlvm7777.cloudapp.net** et un point de terminaison de machine virtuelle **57500**. En supposant que la connectivité correctement configurée, hello suivant de chaîne de connexion peut être utilisé tooaccess hello virtual machine depuis n’importe où sur hello internet :

    "Server=mycloudservice.cloudapp.net,57500;Integrated Security=false;User ID=<login_name>;Password=<your_password>"

Bien que cette chaîne de connexion permet la connectivité des clients sur internet de hello, cela ne signifie pas que tout le monde peut se connecter tooyour SQL Server. Clients externes ont le mot de passe et le nom d’utilisateur correct de toohello. Pour renforcer la sécurité, n’utilisez pas le port connu hello 1433 pour point de terminaison hello publique machine virtuelle. Et, si possible, envisagez d’ajouter une ACL sur votre point de terminaison toorestrict trafic toohello uniquement les clients que vous autoriser. Pour obtenir des instructions sur l’utilisation de listes ACL avec points de terminaison, consultez [gérer hello ACL sur un point de terminaison](../classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).

> [!NOTE]
> Lorsque vous utilisez cette technique toocommunicate avec SQL Server, toutes les données sortantes à partir de hello centre de données Azure est sujet toonormal [tarification des transferts de données sortantes](https://azure.microsoft.com/pricing/details/data-transfers/).
> 
> 

### <a name="connect-toosql-server-in-hello-same-virtual-network"></a>Se connecter tooSQL Server Bonjour même réseau virtuel
[réseau virtuel](../../../virtual-network/virtual-networks-overview.md) offre des scénarios supplémentaires. Vous pouvez connecter des machines virtuelles dans le même réseau virtuel, même si ces ordinateurs virtuels existent dans différents services cloud de hello. De plus, un [VPN de site à site](../../../vpn-gateway/vpn-gateway-site-to-site-create.md)permet de créer une architecture hybride qui connecte les machines virtuelles aux machines et réseaux locaux.

Réseaux virtuels également activer vous toojoin votre domaine tooa de machines virtuelles Azure. Jointure tooa domaine est hello seule façon toouse l’authentification Windows avec SQL Server. Hello autres scénarios de connexion requièrent l’authentification SQL avec des noms d’utilisateur et mots de passe.

Si vous envisagez de tooconfigure un environnement de domaine et l’authentification Windows, il est inutile hello l’authentification SQL ou point de terminaison public tooconfigure hello et des connexions. Dans ce scénario, vous pouvez connecter l’instance de SQL Server tooyour en spécifiant le nom de machine virtuelle SQL Server hello dans la chaîne de connexion hello. Bonjour à l’exemple suivant suppose que l’authentification Windows a été configurée et que cet utilisateur hello a été accordé l’instance de SQL Server toohello accès.

    "Server=mysqlvm;Integrated Security=true"

## <a name="steps-for-configuring-sql-server-connectivity-in-an-azure-vm"></a>Procédure de configuration de la connectivité SQL Server dans une machine virtuelle Azure
Hello suit montrent comment instance de SQL Server tooconnect toohello sur hello internet à l’aide de SQL Server Management Studio (SSMS). Toutefois, hello même procédure s’applique toomaking votre ordinateur de virtuel SQL Server accessible pour vos applications en cours d’exécution à la fois localement et dans Azure.

Avant de pouvoir connecter l’instance toohello de SQL Server à partir d’une autre machine virtuelle ou hello internet, vous devez effectuer hello tâches suivantes :

* [Créer un point de terminaison TCP pour la machine virtuelle de hello](#create-a-tcp-endpoint-for-the-virtual-machine)
* [Ouvrez les ports TCP dans le pare-feu Windows hello](#open-tcp-ports-in-the-windows-firewall-for-the-default-instance-of-the-database-engine)
* [Configurer SQL Server toolisten sur hello protocole TCP](#configure-sql-server-to-listen-on-the-tcp-protocol)
* [Configurer SQL Server pour l’authentification en mode mixte](#configure-sql-server-for-mixed-mode-authentication)
* [Créer des connexions d’authentification SQL Server](#create-sql-server-authentication-logins)
* [Déterminer le nom DNS de hello de machine virtuelle de hello](#determine-the-dns-name-of-the-virtual-machine)
* [Se connecter toohello du moteur de base de données à partir d’un autre ordinateur](#connect-to-the-database-engine-from-another-computer)

chemin d’accès de connexion Hello est résumée par hello suivant schéma :

![Connexion de machine virtuelle de SQL Server tooa](../../../../includes/media/virtual-machines-sql-server-connection-steps/SQLServerinVMConnectionMap.png)

[!INCLUDE [Connect tooSQL Server in a VM Classic TCP Endpoint](../../../../includes/virtual-machines-sql-server-connection-steps-classic-tcp-endpoint.md)]

[!INCLUDE [Connect tooSQL Server in a VM](../../../../includes/virtual-machines-sql-server-connection-steps.md)]

[!INCLUDE [Connect tooSQL Server in a VM Classic Steps](../../../../includes/virtual-machines-sql-server-connection-steps-classic.md)]

## <a name="next-steps"></a>Étapes suivantes
Si vous prévoyez également toouse des groupes de disponibilité AlwaysOn pour une haute disponibilité et récupération d’urgence, vous devez envisager d’implémenter un écouteur. Les clients de base de données connectent toohello écouteur plutôt que directement tooone des instances de SQL Server hello. Hello écouteur itinéraires clients toohello réplica principal dans le groupe de disponibilité hello. Pour plus d’informations, voir [Configuration d’un écouteur à équilibrage de charge interne pour des groupes de disponibilité AlwaysOn dans Azure](../classic/ps-sql-int-listener.md).

Il est important tooreview que tous hello meilleures pratiques de sécurité pour SQL Server s’exécutant sur une machine virtuelle Azure. Pour plus d’informations, consultez [Considérations relatives à la sécurité de SQL Server sur les machines virtuelles Azure](../sql/virtual-machines-windows-sql-security.md).

[Explorer hello cursus](https://azure.microsoft.com/documentation/learning-paths/sql-azure-vm/) pour SQL Server sur des machines virtuelles. 

Pour les autres rubriques connexes toorunning SQL Server dans des machines virtuelles Azure, consultez [SQL Server sur des Machines virtuelles Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

