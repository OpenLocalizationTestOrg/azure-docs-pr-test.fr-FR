---
title: "aaaViewing et modification des noms d’hôtes | Documents Microsoft"
description: "Comment tooview et modification des noms d’hôte pour les machines virtuelles, web et rôles de travail pour la résolution de noms"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: c668cd8e-4e43-4d05-acc3-db64fa78d828
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2016
ms.author: jdial
ms.openlocfilehash: 17d0dd7911754a94db3f37b924b4687da1c70aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="viewing-and-modifying-hostnames"></a>Affichage et modification des noms d'hôtes
tooallow votre toobe d’instances de rôle référencés par nom d’hôte, vous devez définir la valeur hello hello nom d’hôte dans le fichier de configuration de service hello pour chaque rôle. Pour ce faire, ajout hello souhaité hôte nom toohello **vmName** attribut Hello **rôle** élément. Hello valeur Hello **vmName** attribut est utilisé comme base pour le nom d’hôte hello de chaque instance de rôle. Par exemple, si **vmName** est *webrole* et il existe trois instances de ce rôle, les noms d’hôte hello d’instances de hello sera *webrole0*, *webrole1* , et *webrole2*. Vous n’avez pas besoin de toospecify un nom d’hôte pour les ordinateurs virtuels dans le fichier de configuration de hello, car le nom d’hôte hello pour un ordinateur virtuel est rempli en fonction du nom d’ordinateur virtuel hello. Pour en savoir plus sur la configuration d’un service Microsoft Azure, consultez la section [Schéma de configuration du service Azure (fichier .cscfg)](https://msdn.microsoft.com/library/azure/ee758710.aspx)

## <a name="viewing-hostnames"></a>Affichage des noms d’hôtes
Vous pouvez afficher les noms d’hôte hello des machines virtuelles et instances de rôle dans un service cloud à l’aide des outils hello ci-dessous.

### <a name="azure-portal"></a>Portail Azure
Vous pouvez utiliser hello [portail Azure](http://portal.azure.com) noms d’hôte tooview hello pour les ordinateurs virtuels sur le panneau de vue d’ensemble de hello pour un ordinateur virtuel. N’oubliez pas que hello panneau affiche une valeur pour **nom** et **nom d’hôte**. Bien que ces valeurs sont initialement hello identiques, la modification du nom d’hôte hello ne modifie pas de nom de hello de machine virtuelle de hello ou instance de rôle.

Instances de rôle peuvent également être affichées dans hello portail Azure, mais lorsque vous répertoriez les instances hello dans un service cloud, nom d’hôte hello ne figure pas. Vous verrez un nom pour chaque instance, mais ce nom ne représente pas de nom d’hôte hello.

### <a name="service-configuration-file"></a>Fichier de configuration de service
Vous pouvez télécharger le fichier de configuration de service hello pour un service déployé à partir de hello **configurer** Panneau de service hello Bonjour portail Azure. Vous pouvez ensuite rechercher hello **vmName** attribut pour hello **nom de rôle** nom d’hôte d’élément toosee hello. Gardez à l’esprit que ce nom d’hôte est utilisé comme base pour le nom d’hôte hello de chaque instance de rôle. Par exemple, si **vmName** est *webrole* et il existe trois instances de ce rôle, les noms d’hôte hello d’instances de hello sera *webrole0*, *webrole1* , et *webrole2*.

### <a name="remote-desktop"></a>Bureau à distance
Après avoir activé le Bureau à distance (Windows), la communication à distance de Windows PowerShell (Windows), ou virtuels tooyour de connexions SSH (Linux et Windows) ou instances de rôle, vous pouvez afficher le nom d’hôte hello à partir d’une connexion Bureau à distance active de différentes manières :

* Tapez le nom d’hôte à l’invite de commandes hello ou terminal SSH.
* Tapez ipconfig/tout à la commande hello invite de commandes (Windows uniquement).
* Affichez le nom hello dans le système de hello paramètres (Windows uniquement).

### <a name="azure-service-management-rest-api"></a>API REST de gestion des services Azure
À partir d’un client REST. suivez ces instructions :

1. Assurez-vous que vous disposez d’un ordinateur client certificat tooconnect toohello portail Azure. tooobtain un certificat client, suivez les étapes de hello présentées dans [Comment : télécharger et importer les paramètres de publication et les informations d’abonnement](https://msdn.microsoft.com/library/dn385850.aspx). 
2. Définissez une entrée d’en-tête intitulée x-ms-version , présentant une valeur de 2013-11-01.
3. Envoyez une demande hello suivant le format : https://management.core.windows.net/\<subscrition-id\>/services/hostedservices/\<-nom du service\>? détail incorporer = true
4. Recherchez hello **nom d’hôte** élément pour chaque **RoleInstance** élément.

> [!WARNING]
> Vous pouvez également afficher le suffixe de domaine interne hello pour votre service cloud à partir de la réponse à un appel REST de hello en vérifiant hello **InternalDnsSuffix** élément, ou en exécutant ipconfig/à partir d’une invite de commandes dans une session Bureau à distance (Windows) ou en cours d’exécution /etc/resolv.conf cat à partir d’un terminal SSH (Linux).
> 
> 

## <a name="modifying-a-hostname"></a>Modification d’un nom d’hôte
Vous pouvez modifier le nom d’hôte hello pour n’importe quel ordinateur virtuel ou d’une instance de rôle en téléchargeant un fichier de configuration de service modifié ou en renommant l’ordinateur hello à partir d’une session Bureau à distance.

## <a name="next-steps"></a>Étapes suivantes
[Résolution de noms pour les machines virtuelles et les instances de rôle](virtual-networks-name-resolution-for-vms-and-role-instances.md)

[Schéma de configuration de service Azure (.cscfg)](https://msdn.microsoft.com/library/windowsazure/ee758710.aspx)

[Schéma de configuration du réseau virtuel Azure](http://go.microsoft.com/fwlink/?LinkId=248093)

[Définir les paramètres DNS à l'aide de fichiers de configuration réseau](virtual-networks-specifying-a-dns-settings-in-a-virtual-network-configuration-file.md)

