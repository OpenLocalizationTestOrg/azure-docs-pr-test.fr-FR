---
title: "aaaHow toocreate, gérer ou supprimer un compte de stockage Bonjour portail Azure | Documents Microsoft"
description: "Créer un nouveau compte de stockage, gérez vos clés d’accès de compte ou supprimer un compte de stockage Bonjour portail Azure. En savoir plus sur les comptes de stockage standard et Premium."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 87c37da0-6cc6-4d88-a330-ef2896a1531d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
f1_keywords: sql13.swb.windowsazurestorage.connect.f1
ms.date: 01/23/2017
ms.author: robinsh
ms.openlocfilehash: 3a2a07c4131fbe594c7007f59950bf94339809fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="about-azure-storage-accounts"></a>À propos des comptes de stockage Azure
[!INCLUDE [storage-selector-portal-create-storage-account](../../../includes/storage-selector-portal-create-storage-account.md)]

[!INCLUDE [storage-table-cosmos-db-tip-include](../../../includes/storage-table-cosmos-db-tip-include.md)]

## <a name="overview"></a>Vue d'ensemble
Un compte de stockage Azure fournit un toostore de l’espace de noms unique et accéder à vos objets de données de stockage Azure. Tous les objets d’un compte de stockage sont facturés ensemble en tant que groupe. Par défaut, les données de salutation dans votre compte sont disponible tooyou uniquement, propriétaire du compte hello.

[!INCLUDE [storage-account-types-include](../../../includes/storage-account-types-include.md)]

## <a name="storage-account-billing"></a>Facturation du compte de stockage
[!INCLUDE [storage-account-billing-include](../../../includes/storage-account-billing-include.md)]

> [!NOTE]
> Lorsque vous créez une machine virtuelle Azure, un compte de stockage est créé pour vous automatiquement dans l’emplacement de déploiement hello si vous n’avez pas déjà un compte de stockage à cet emplacement. Par conséquent, il n’est pas nécessaire toofollow les étapes de hello ci-dessous toocreate un compte de stockage pour vos disques de machine virtuelle. nom de compte de stockage Hello doit reposer sur le nom d’ordinateur virtuel hello. Consultez hello [des Machines virtuelles Azure documentation](https://azure.microsoft.com/documentation/services/virtual-machines/) pour plus d’informations.
> 
> 

## <a name="storage-account-endpoints"></a>Points de terminaison d'un compte de stockage
Chaque objet que vous stockez dans Azure Storage possède une adresse URL unique. formulaires de nom de compte de stockage Hello hello sous-domaine de cette adresse. Hello combinaison de sous-domaine et nom de domaine, qui est un service de tooeach spécifique, forme un *point de terminaison* pour votre compte de stockage.

Par exemple, si votre compte de stockage nommé *mystorageaccount*, sont des points de terminaison hello par défaut pour votre compte de stockage :

* Service BLOB : http://*mystorageaccount*.blob.core.windows.net
* Service de Table : http://*moncomptedestockage*.table.core.windows.net
* Service de File d’attente : http://*moncomptedestockage*.queue.core.windows.net
* Service de fichiers : http://*mystorageaccount*.file.core.windows.net

> [!NOTE]
> Un compte de stockage d’objets Blob expose uniquement un point de terminaison de service hello Blob.
> 
> 

URL de Hello pour accéder à un objet dans un compte de stockage est créé en ajoutant l’emplacement de l’objet hello dans le point de terminaison toohello hello stockage compte. Par exemple, une adresse d’objet blob peut avoir ce format : http://*moncomptedestockage*.blob.core.windows.net/*monconteneur*/*monobjetblob*.

Vous pouvez également configurer un toouse de nom de domaine personnalisé avec votre compte de stockage. Pour plus d’informations, consultez la page [Configurer un nom de domaine personnalisé pour un point de terminaison Blob Storage](../blobs/storage-custom-domain-name.md). Vous pouvez également le configurer avec PowerShell. Pour plus d’informations, consultez hello [Set-AzureRmStorageAccount](/powershell/module/azurerm.storage/set-azurermstorageaccount) applet de commande.  


## <a name="create-a-storage-account"></a>Créez un compte de stockage.
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Dans le menu du Hub hello, sélectionnez **nouveau** -> **stockage** -> **compte de stockage**.
3. Entrez un nom pour votre compte de stockage. Consultez [points de terminaison de stockage compte](#storage-account-endpoints) pour des détails sur comment le nom de compte de stockage hello sera utilisé tooaddress vos objets dans le stockage Azure.
   
   > [!NOTE]
   > Les noms des comptes de stockage doivent comporter entre 3 et 24 caractères, uniquement des lettres minuscules et des chiffres.
   > 
   > Le nom de votre compte de stockage doit être unique dans Azure. Hello portail Azure indique si le nom de compte de stockage hello que vous sélectionnez est déjà en cours d’utilisation.
   > 
   > 
4. Spécifiez toobe de modèle de déploiement hello utilisé : **le Gestionnaire de ressources** ou **classique**. **Le Gestionnaire de ressources** hello est recommandé de modèle de déploiement. Pour plus d’informations, consultez [Présentation du déploiement de Resource Manager et du déploiement classique](../../azure-resource-manager/resource-manager-deployment-model.md).
   
   > [!NOTE]
   > Comptes de stockage d’objets BLOB ne peuvent être créés à l’aide du modèle de déploiement du Gestionnaire de ressources hello.

5. Sélectionnez le type hello du compte de stockage : **usage général** ou **stockage d’objets Blob**. **Usage général** est la valeur par défaut hello.
   
    Si **usage général** a été sélectionné, puis spécifiez le niveau de performances de hello : **Standard** ou **Premium**. valeur par défaut Hello est **Standard**. Pour plus d’informations sur les comptes de stockage standard et premium, consultez [Introduction tooMicrosoft Azure Storage](storage-introduction.md) et [stockage Premium : stockage hautes performances pour les charges de travail de Machine virtuelle Azure](storage-premium-storage.md).
   
    Si **stockage d’objets Blob** a été sélectionné, puis spécifiez le niveau d’accès hello : **à chaud** ou **froid**. valeur par défaut Hello est **à chaud**. Pour plus d’informations, voir [Stockage d’objets blob Azure : niveaux froid et chaud](../blobs/storage-blob-storage-tiers.md) .
6. Sélectionnez l’option de réplication hello pour le compte de stockage hello : **LRS**, **GRS**, **RA-GRS**, ou **ZRS**. valeur par défaut Hello est **RA-GRS**. Pour plus d’informations sur les options de réplication d’Azure Storage, consultez [Réplication Azure Storage](storage-redundancy.md).
7. Sélectionnez l’abonnement hello dans lequel vous souhaitez toocreate hello nouveau compte de stockage.
8. Spécifiez un nouveau groupe de ressources ou sélectionnez un groupe de ressources existant. Pour plus d’informations sur les groupes de ressources, consultez [Vue d’ensemble d’Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).
9. Sélectionnez l’emplacement géographique de hello pour votre compte de stockage. Pour plus d’informations sur les services disponibles dans chaque région, voir [Régions Azure](https://azure.microsoft.com/regions/#services) .
10. Cliquez sur **créer** compte de stockage toocreate hello.

## <a name="manage-your-storage-account"></a>Gérer votre compte de stockage
### <a name="change-your-account-configuration"></a>Modifier la configuration de votre compte
Après avoir créé votre compte de stockage, vous pouvez modifier sa configuration, telles que la modification d’option de réplication hello utilisée pour le compte de hello ou de la couche d’accès aux variables hello pour un compte de stockage d’objets Blob. Bonjour [portail Azure](https://portal.azure.com), accédez de compte de stockage tooyour, recherchez et cliquez sur **Configuration** sous **paramètres** tooview et/ou de la modification de configuration de compte hello.

> [!NOTE]
> Selon le niveau de performances hello choisis lors de la création du compte de stockage hello, certaines options de réplication n’est peut-être pas disponibles.
> 
> 

L’option de réplication hello modification affecte la tarification. Pour plus d’informations, voir [Tarification Azure Storage](https://azure.microsoft.com/pricing/details/storage/) .

Pour l’objet Blob de comptes de stockage, la modification du niveau d’accès hello peuvent entraîner une baisse des frais pour hello modifier en plus toochanging le tarif. Consultez hello [comptes - tarification et facturation de stockage d’objets Blob](../blobs/storage-blob-storage-tiers.md#pricing-and-billing) pour plus d’informations.

### <a name="manage-your-storage-access-keys"></a>Gérer vos clés d’accès de stockage
Lorsque vous créez un compte de stockage, Azure génère deux clés d’accès stockage 512 bits, qui sont utilisées pour l’authentification lors de l’accès au compte de stockage hello. En fournissant deux clés d’accès de stockage, Azure vous permet de clés de hello tooregenerate avec aucun service de stockage tooyour d’interruption ou le service d’accès toothat.

> [!NOTE]
> Nous vous recommandons d’éviter de partager vos clés d’accès de stockage avec qui que ce soit. toopermit accès toostorage ressources sans vous communiquez vos clés d’accès, vous pouvez utiliser un *signature d’accès partagé*. Une signature d’accès partagé fournit des ressources de tooa d’accès dans votre compte pour un intervalle que vous définissez et avec les autorisations hello que vous spécifiez. Pour plus d’informations, consultez [Utilisation des signatures d’accès partagé (SAP)](storage-dotnet-shared-access-signature-part-1.md) .
> 
> 
<a id="view-and-copy-storage-access-keys"/></a>
#### <a name="view-and-copy-storage-access-keys"></a>Afficher et copier les clés d’accès de stockage
Bonjour [portail Azure](https://portal.azure.com), accédez de compte de stockage tooyour, cliquez sur **tous les paramètres** puis cliquez sur **clés d’accès** tooview, copier et régénérer vos clés d’accès de compte. Hello **clés d’accès** panneau inclut également des chaînes de connexion préconfigurée de manière à l’aide de vos clés primaires et secondaires, vous pouvez ainsi copier toouse dans vos applications.

#### <a name="regenerate-storage-access-keys"></a>Régénération des clés d'accès de stockage
Nous vous recommandons de modifier les clés d’accès hello tooyour du compte de stockage régulièrement conserver toohelp vos connexions de stockage sécurisé. Deux clés d’accès sont affectés afin que vous pouvez conserver compte de stockage toohello de connexions à l’aide d’une clé d’accès pendant la régénération de hello autre clé d’accès.

> [!WARNING]
> Régénérer vos clés d’accès peut affecter les services dans Azure, ainsi que vos propres applications qui dépendent de compte de stockage hello. Tous les clients qui utilisent le compte de stockage hello hello accès tooaccess clé doivent être mis à jour toouse clé hello.
> 
> 

**Les services de support** -si vous avez des services de support qui dépendent de votre compte de stockage, vous devez resynchroniser les clés d’accès hello avec votre service multimédia après avoir régénéré les clés de hello.

**Applications** : Si vous possédez des applications web ou de services de cloud computing que hello utiliser le compte de stockage, vous allez perdre les connexions hello si vous régénérez des clés, sauf si vous régénérez vos clés.

**Explorateurs de stockage** : Si vous utilisez une [applications de l’Explorateur de stockage](storage-explorers.md), vous devrez probablement tooupdate hello la clé utilisée par ces applications.

Voici le processus de hello rotation de vos clés d’accès de stockage :

1. Mettre à jour les chaînes de connexion hello dans votre clé d’accès secondaire application code tooreference hello hello du compte de stockage.
2. Régénérer la clé d’accès primaire hello pour votre compte de stockage. Sur hello **clés d’accès** panneau, cliquez sur **Key1 de régénérer**, puis cliquez sur **Oui** tooconfirm que vous souhaitez toogenerate une nouvelle clé.
3. Mettre à jour les chaînes de connexion hello dans votre code tooreference hello nouvelle clé primaire.
4. Accès secondaire de hello régénérer la clé Bonjour même manière.

## <a name="delete-a-storage-account"></a>Suppression d'un compte de stockage
tooremove un compte de stockage que vous n’utilisez plus, accédez à compte de stockage toohello Bonjour [portail Azure](https://portal.azure.com), puis cliquez sur **supprimer**. Suppression d’un compte de stockage supprime de compte hello, y compris toutes les données dans le compte de hello.

> [!WARNING]
> Il est toorestore n’est pas possible à un compte de stockage supprimé ou récupérer le contenu hello qu’il contenait avant la suppression. Être tooback que rien souhaité toosave avant de supprimer le compte de hello. Cela est également vrai pour toutes les ressources dans le compte de hello, lorsque vous supprimez un objet blob, table, file d’attente ou un fichier, celui-ci est définitivement supprimé.
> 

Si vous essayez toodelete un compte de stockage associé à une machine virtuelle Azure, vous pouvez obtenir une erreur sur le compte de stockage hello toujours en cours d’utilisation. Si vous avez besoin d’aide pour résoudre cette erreur, consultez [Troubleshoot errors when you delete storage accounts](../common/storage-resource-manager-cannot-delete-storage-account-container-vhd.md) (Résoudre les erreurs liées à la suppression de compte de stockage).

## <a name="next-steps"></a>Étapes suivantes
* [Microsoft Azure Storage Explorer](../../vs-azure-tools-storage-manage-with-storage-explorer.md) est une application autonome gratuit, à partir de Microsoft qui vous permet de toowork visuellement avec des données de stockage Azure sur Windows, Mac OS et Linux.
* [Stockage d’objets blob Azure : niveaux froid et chaud](../blobs/storage-blob-storage-tiers.md)
* [Réplication Azure Storage](storage-redundancy.md)
* [Configuration des chaînes de connexion Azure Storage](../storage-configure-connection-string.md)
* [Transfert de données avec l’utilitaire de ligne de commande AzCopy de hello](storage-use-azcopy.md)
* Visitez hello [Blog de l’équipe stockage Azure](http://blogs.msdn.com/b/windowsazurestorage/).

