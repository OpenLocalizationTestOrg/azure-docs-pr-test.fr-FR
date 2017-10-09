---
title: "aaaSecurity considérations pour SQL Server dans Azure | Documents Microsoft"
description: "Cette rubrique fournit des instructions générales pour la sécurisation de SQL Server en cours d’exécution sur une machine virtuelle Azure."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: d710c296-e490-43e7-8ca9-8932586b71da
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/02/2017
ms.author: jroth
ms.openlocfilehash: 14c3d828fa87446da67beea6d28886de254afe15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="security-considerations-for-sql-server-in-azure-virtual-machines"></a>Considérations relatives à la sécurité de SQL Server sur les machines virtuelles Azure

Cette rubrique inclut des instructions de sécurité générales pour créer des instances de serveur tooSQL un accès sécurisé dans une machine virtuelle Azure (VM).

Azure est conforme à plusieurs réglementations du secteur et les normes que vous peuvent activer toobuild une solution conforme avec SQL Server est en cours d’exécution sur un ordinateur virtuel. Pour plus d’informations sur les exigences réglementaires relatives à Azure, voir [Centre de confidentialité Azure](https://azure.microsoft.com/support/trust-center/).

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="control-access-toohello-sql-vm"></a>Contrôle l’accès toohello SQL VM

Lorsque vous créez votre machine virtuelle SQL Server, envisagez comment toocarefully contrôler l’ordinateur de toohello d’accès et tooSQL Server. En règle générale, vous devez effectuer les suivant hello :

- Restreindre l’accès tooSQL Server tooonly hello applications et les clients qui en ont besoin.
- Suivre les meilleures pratiques de gestion des comptes d’utilisateur et des mots de passe.

Hello les sections suivantes fournit des suggestions de réfléchir à ces points.

## <a name="secure-connections"></a>Sécuriser les connexions

Lorsque vous créez une machine virtuelle SQL Server avec une image de la galerie, hello **connectivité SQL Server** option donne hello de choix de **Local (à l’intérieur de la machine virtuelle)**, **privé (dans le réseau virtuel)** , ou **Public (Internet)**.

![Connectivité SQL Server](./media/virtual-machines-windows-sql-security/sql-vm-connectivity-option.png)

Pour une sécurité optimale hello, choisissez l’option la plus restrictive hello pour votre scénario. Par exemple, si vous exécutez une application qui accède à SQL Server sur hello même machine virtuelle, puis **Local** est l’option la plus sûre hello. Si vous exécutez une application Azure qui nécessite l’accès toohello SQL Server, puis **privé** sécurise la communication tooSQL serveur uniquement au sein de hello spécifié [réseau virtuel Azure](../../../virtual-network/virtual-networks-overview.md). Si vous avez besoin **Public** (internest) accès toohello machine virtuelle SQL Server, puis assurez-vous de toofollow que des autres meilleures pratiques dans cette rubrique tooreduce votre surface d’attaque.

Hello des options sélectionnées dans le portail de hello utilisent les règles de sécurité de trafic entrant sur les machines virtuelles de hello [groupe de sécurité réseau](../../../virtual-network/virtual-networks-nsg.md) (NSG) tooallow ou refuser la machine virtuelle de réseau du trafic tooyour. Vous pouvez modifier ou créer des règles de groupe de sécurité réseau entrants du port de SQL Server toohello tooallow le trafic en (1433 par défaut). Vous pouvez également spécifier des adresses IP spécifiques autorisées toocommunicate sur ce port.

![Règles de groupe de sécurité réseau](./media/virtual-machines-windows-sql-security/sql-vm-network-security-group-rules.png)

En outre tooNSG règles toorestrict du trafic réseau, vous pouvez également utiliser hello le pare-feu Windows sur l’ordinateur virtuel de hello.

Si vous utilisez des points de terminaison avec le modèle de déploiement classique de hello, supprimez les points de terminaison sur l’ordinateur virtuel de hello si vous ne les utilisez pas. Pour obtenir des instructions sur l’utilisation de listes ACL avec points de terminaison, consultez [gérer hello ACL sur un point de terminaison](../classic/setup-endpoints.md#manage-the-acl-on-an-endpoint). Cela n’est pas nécessaire pour les machines virtuelles qui utilisent le Gestionnaire de ressources de hello.

Enfin, envisagez d’activer des connexions chiffrées d’instance hello Hello du moteur de base de données SQL Server dans votre machine virtuelle Azure. Configurez l’instance SQL Server avec un certificat signé. Pour plus d’informations, consultez [toohello d’activer les connexions chiffrées du moteur de base de données](https://docs.microsoft.com/sql/database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine) et [syntaxe de chaîne de connexion](https://msdn.microsoft.com/library/ms254500.aspx).

## <a name="use-a-non-default-port"></a>Utiliser un port non défini par défaut

Par défaut, SQL Server écoute un port bien connu, le port 1433. Pour renforcer la sécurité, configurez toolisten de SQL Server sur un port non défini par défaut, tels que 1401. Si vous configurez une image de la galerie de SQL Server dans hello portail Azure, vous pouvez spécifier ce port dans hello **paramètres SQL Server** panneau.

tooconfigure cette après le déploiement, vous avez deux options :

- Pour les machines virtuelles du Gestionnaire de ressources, vous pouvez sélectionner **configuration de SQL Server** à partir du Panneau de vue d’ensemble d’ordinateurs virtuels hello. Cela fournit une option de port de hello toochange.

  ![Modification du port TCP dans le portail](./media/virtual-machines-windows-sql-security/sql-vm-change-tcp-port.png)

- Pour les machines virtuelles classique ou pour les machines virtuelles SQL Server qui n’ont pas configuré avec le portail de hello, vous pouvez configurer manuellement le port de hello en vous connectant à distance toohello machine virtuelle. Pour les étapes de configuration hello, consultez [configurer un serveur tooListen sur un Port TCP spécifique](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port). Si vous utilisez cette technique manuelle, vous devez également tooadd un pare-feu Windows règle tooallow le trafic entrant sur ce port TCP.

> [!IMPORTANT]
> Spécification d’un port par défaut d’est une bonne idée si le port de SQL Server est toopublic ouvrir des connexions internet.

Lorsque SQL Server est à l’écoute sur un port non défini par défaut, vous devez spécifier les ports hello lorsque vous vous connectez. Par exemple, considérez un scénario où adresse IP du serveur hello est 13.55.255.255 et SQL Server est à l’écoute sur le port 1401. tooconnect tooSQL serveur, vous devez spécifier `13.55.255.255,1401` dans la chaîne de connexion hello.

## <a name="manage-accounts"></a>Gérer les comptes

Vous ne souhaitez pas les mots de passe ou les noms des comptes des personnes malveillantes tooeasily estimation. Utilisez hello suivant les conseils toohelp :

- Créez un seul compte d’administrateur local avec un nom différent de **Administrator**.

- Utilisez des mots de passe forts complexes pour tous vos comptes. Pour plus d’informations sur la façon toocreate un mot de passe fort, consultez [créer un mot de passe fort](https://support.microsoft.com/instantanswers/9bd5223b-efbe-aa95-b15a-2fb37bef637d/create-a-strong-password) l’article.

- Par défaut, Azure sélectionne l’authentification Windows pendant l’installation de la machine virtuelle SQL Server. Par conséquent, hello **SA** connexion est désactivée et un mot de passe est attribué par le programme d’installation. Nous recommandons que hello **SA** connexion ne doit pas utilisée ni activée. Si vous devez avoir une connexion SQL, utilisez une des hello suivant des stratégies :

  - Créez un compte SQL avec un nom unique et qui est membre de **sysadmin**. Cela en permettant à partir du portail de hello **l’authentification SQL** lors de la configuration.

    > [!TIP] 
    > Si vous n’activez pas l’authentification SQL lors de la configuration, vous devez modifier manuellement le mode d’authentification hello trop**SQL Server et le Mode d’authentification Windows**. Pour plus d’informations, consultez [Modifier le mode d’authentification du serveur](https://docs.microsoft.com/sql/database-engine/configure-windows/change-server-authentication-mode).

  - Si vous devez utiliser hello **SA** connexion, connexion de hello activer après la mise en service et attribuer un nouveau mot de passe fort.

## <a name="follow-on-premises-best-practices"></a>Suivre les meilleures pratiques locales

En outre toohello pratiques décrites dans cette rubrique, nous recommandons que vous passez en revue et mettre en œuvre les pratiques de sécurité locales traditionnelles hello le cas échéant. Pour plus d’informations, consultez [Considérations sur la sécurité pour une installation SQL Server](https://docs.microsoft.com/sql/sql-server/install/security-considerations-for-a-sql-server-installation)

## <a name="next-steps"></a>Étapes suivantes

Si vous vous intéressez également à l’optimisation des performances, voir [Meilleures pratiques relatives aux performances de SQL Server sur les machines virtuelles Azure](virtual-machines-windows-sql-performance.md).

Pour les autres rubriques connexes toorunning SQL Server dans des machines virtuelles Azure, consultez [SQL Server sur une vue d’ensemble des Machines virtuelles Azure](virtual-machines-windows-sql-server-iaas-overview.md).

