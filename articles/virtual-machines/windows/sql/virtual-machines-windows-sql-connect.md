---
title: aaaConnect tooa Machine virtuelle de SQL Server (Gestionnaire de ressources) | Documents Microsoft
description: "Découvrez comment tooconnect tooSQL Server en cours d’exécution sur un ordinateur virtuel dans Azure. Cette rubrique utilise le modèle de déploiement classique hello. scénarios de Hello diffèrent en fonction de la configuration du réseau hello et l’emplacement de hello du client de hello."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-resource-manager
ms.assetid: aa5bf144-37a3-4781-892d-e0e300913d03
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/14/2017
ms.author: jroth
ms.openlocfilehash: 7b127c14c37b9a72c19ed17f8b1dad61c7bc2d38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-sql-server-virtual-machine-on-azure-resource-manager"></a>Se connecter tooa Machine virtuelle de SQL Server sur Azure (Resource Manager).
> [!div class="op_single_selector"]
> * [Gestionnaire de ressources](virtual-machines-windows-sql-connect.md)
> * [Classique](../classic/sql-connect.md)
> 
> 

## <a name="overview"></a>Vue d'ensemble

Cette rubrique décrit comment tooconnect tooyour SQL Server de l’instance en cours d’exécution sur une machine virtuelle Azure. Elle aborde certains [scénarios de connectivité générale](#connection-scenarios) et fournit une [procédure détaillée pour configurer la connectivité à SQL Server dans une machine virtuelle Azure](#steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm).

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

Si vous préférez suivre une procédure pas-à-pas complète d’approvisionnement et de connectivité, voir [Approvisionnement d’une machine virtuelle SQL Server dans Azure](virtual-machines-windows-portal-sql-server-provision.md).

## <a name="connection-scenarios"></a>Scénarios de connexion

moyen de Hello un client connecte tooSQL Server s’exécutant sur un ordinateur virtuel diffère selon l’emplacement de hello du client de hello et configuration de réseau de hello.

Si vous configurez un ordinateur virtuel SQL Server Bonjour portail Azure, vous pouvez hello de spécification de type hello de **connectivité SQL**.

![Option de connectivité SQL publique lors de l’approvisionnement](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity.png)

Les options de connectivité sont les suivantes :

| Option | Description |
|---|---|
| **Public** | Se connecter tooSQL Server sur hello internet |
| **Privé** | Se connecter tooSQL Server Bonjour même réseau virtuel |
| **Local** | Se connecter tooSQL Server localement sur hello même machine virtuelle | 

Hello sections suivantes expliquent hello **Public** et **privé** options plus en détail.

## <a name="connect-toosql-server-over-hello-internet"></a>Se connecter tooSQL Server sur hello Internet

Si vous souhaitez que le moteur de base de données SQL Server tooconnect tooyour de hello Internet, sélectionnez **Public** pour hello **connectivité SQL** type dans le portail hello lors de la configuration. portail de Hello automatiquement hello comme suit :

* Active le protocole TCP/IP hello pour SQL Server.
* Configure un Bonjour de tooopen de règle de pare-feu le port TCP du serveur SQL (1433 par défaut).
* Il active l’authentification SQL Server, requis pour l’accès public.
* Configure un groupe de sécurité réseau hello sur hello VM tooall TCP le trafic sur hello port SQL Server.

> [!IMPORTANT]
> les éditions Express et les images de machine virtuelle Hello pourquoi SQL Server Developer n’activent pas automatiquement de protocole de hello TCP/IP. Pour les éditions développeur et Express, vous devez utiliser le Gestionnaire de Configuration SQL Server trop[activer manuellement le protocole de hello TCP/IP](#manualtcp) après la création d’hello machine virtuelle.

N’importe quel client ayant accès à internet peut se connecter à instance de SQL Server toohello en spécifiant hello adresse IP publique de machine virtuelle de hello ou n’importe quel nom DNS adresse IP de toothat. Si hello port SQL Server est 1433, vous n’avez pas besoin de toospecify dans la chaîne de connexion hello. Hello suivant de chaîne de connexion connecte tooa SQL VM avec un nom DNS de `sqlvmlabel.eastus.cloudapp.azure.com` à l’aide de l’authentification SQL (vous pouvez utiliser également l’adresse IP publique de hello).

```
Server=sqlvmlabel.eastus.cloudapp.azure.com;Integrated Security=false;User ID=<login_name>;Password=<your_password>
```

Bien que cela permet la connectivité pour les clients sur internet de hello, cela ne signifie pas que tout le monde peut se connecter tooyour SQL Server. Clients externes ont le mot de passe et le nom d’utilisateur correct de toohello. Toutefois, pour renforcer la sécurité, vous pouvez éviter le port connu hello 1433. Par exemple, si vous avez configuré toolisten de SQL Server sur le port 1500 et établi de pare-feu appropriés et règles de groupe de sécurité réseau, vous pouvez connecter en ajoutant le nom du serveur hello port numéro toohello. Hello exemple suivant modifie hello précédent en ajoutant un numéro de port personnalisé, **1500**, nom du serveur toohello :

```
Server=sqlvmlabel.eastus.cloudapp.azure.com,1500;Integrated Security=false;User ID=<login_name>;Password=<your_password>"
```

> [!NOTE]
> Lorsque vous interrogez SQL Server dans une machine virtuelle sur hello internet, toutes les données sortantes à partir de hello Azure datacenter est sujet toonormal [tarification des transferts de données sortantes](https://azure.microsoft.com/pricing/details/data-transfers/).

## <a name="connect-toosql-server-within-a-virtual-network"></a>Se connecter tooSQL Server dans un réseau virtuel

Lorsque vous choisissez **privé** pour hello **connectivité SQL** type dans le portail hello, Azure configure la plupart des paramètres hello identiques trop**Public**. Hello une différence est qu’il n’y a aucune tooallow de règle de groupe de sécurité réseau à l’extérieur du trafic sur le port de SQL Server hello (1433 par défaut).

> [!IMPORTANT]
> les éditions Express et les images de machine virtuelle Hello pourquoi SQL Server Developer n’activent pas automatiquement de protocole de hello TCP/IP. Pour les éditions développeur et Express, vous devez utiliser le Gestionnaire de Configuration SQL Server trop[activer manuellement le protocole de hello TCP/IP](#manualtcp) après la création d’hello machine virtuelle.

La connectivité privée est souvent utilisée conjointement avec [Réseau virtuel](../../../virtual-network/virtual-networks-overview.md) et permet plusieurs scénarios. Vous pouvez connecter des machines virtuelles dans le même réseau virtuel, même si ces ordinateurs virtuels existent dans différents groupes de ressources de hello. De plus, un [VPN de site à site](../../../vpn-gateway/vpn-gateway-site-to-site-create.md)permet de créer une architecture hybride qui connecte les machines virtuelles aux machines et réseaux locaux.

Réseaux virtuels également activer vous toojoin votre domaine tooa de machines virtuelles Azure. Il s’agit de hello seule façon toouse l’authentification Windows tooSQL Server. Hello autres scénarios de connexion requièrent l’authentification SQL avec des noms d’utilisateur et mots de passe.

En supposant que vous avez configuré DNS dans votre réseau virtuel, vous pouvez connecter l’instance de SQL Server tooyour en spécifiant le nom de l’ordinateur hello machine virtuelle SQL Server dans la chaîne de connexion hello. Hello également des exemple suivant suppose que l’authentification Windows a été également configurée et que l’utilisateur hello a reçu l’instance de SQL Server toohello access.

```
Server=mysqlvm;Integrated Security=true
```

## <a id="change"></a>Modifier les paramètres de connectivité SQL

Vous pouvez modifier les paramètres de connectivité hello pour votre machine virtuelle de SQL Server dans hello portail Azure.

1. Bonjour portail Azure, sélectionnez **virtuels**.

2. Sélectionnez votre machine virtuelle SQL Server.

3. Sous **paramètres**, cliquez sur **Configuration de SQL Server**.

4. Hello de modification **le niveau de connectivité SQL** tooyour requis définition. Vous pouvez éventuellement utiliser cette hello toochange de zone port SQL Server ou les paramètres de l’authentification SQL hello.

   ![Modifier la connectivité SQL](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity-change.png)

5. Attendez quelques minutes pour toocomplete de mise à jour hello.

   ![Notification de mise à jour de la machine virtuelle SQL](./media/virtual-machines-windows-sql-connect/sql-vm-updating-notification.png)

## <a id="manualtcp"></a> Activer le protocole TCP/IP pour les éditions Developer et Express

Lorsque vous modifiez les paramètres de connectivité de SQL Server, Azure n’active pas automatiquement le protocole de hello TCP/IP pour les éditions Express et SQL Server Developer. les étapes de Hello ci-dessous expliquent comment toomanually activer TCP/IP afin de pouvoir vous connecter à distance par adresse IP.

Tout d’abord, connectez toohello l’ordinateur SQL Server avec le Bureau à distance.

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-remote-desktop-connect.md)]

Ensuite, activez le protocole TCP/IP de hello avec **Gestionnaire de Configuration SQL Server**.

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-connection-tcp-protocol.md)]

## <a name="connect-with-ssms"></a>Connexion avec SSMS

Hello étapes suivantes montrent comment toocreate un DNS facultatif d’étiquette pour votre machine virtuelle Azure et connectez-vous avec SQL Server Management Studio (SSMS).

[!INCLUDE [Connect tooSQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]

## <a name="next-steps"></a>Étapes suivantes

instructions de configuration toosee en même temps que ces étapes de connectivité, consultez [approvisionnement d’une Machine virtuelle de SQL Server sur Azure](virtual-machines-windows-portal-sql-server-provision.md).

Pour les autres rubriques connexes toorunning SQL Server dans des machines virtuelles Azure, consultez [SQL Server sur des Machines virtuelles Azure](virtual-machines-windows-sql-server-iaas-overview.md).
