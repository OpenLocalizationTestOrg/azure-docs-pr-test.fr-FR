---
title: "aaaHow toocreate, gérer ou supprimer un compte de stockage Bonjour portail classique Azure | Documents Microsoft"
description: "Créer un nouveau compte de stockage, gérez vos clés d’accès de compte ou supprimer un compte de stockage Bonjour portail Azure. En savoir plus sur les comptes de stockage standard et Premium."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 5e4f4360-3f81-4d63-a0b1-e7771b67af11
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/23/2017
ms.author: robinsh
ms.openlocfilehash: 6ee2359e02c7c9e9c111e1fc87a6160bb8b785b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="about-azure-storage-accounts"></a>À propos des comptes de stockage Azure
[!INCLUDE [storage-selector-portal-create-storage-account](../../includes/storage-selector-portal-create-storage-account.md)]

[!INCLUDE [storage-try-azure-tools](../../includes/storage-try-azure-tools.md)]

## <a name="overview"></a>Vue d'ensemble
Un stockage Azure compte vous donne accès toohello des services Azure Blob, file d’attente, Table et fichier dans le stockage Azure. Votre compte de stockage fournit l’espace de noms unique hello pour vos objets de données de stockage Azure. Par défaut, les données de salutation dans votre compte sont disponible tooyou uniquement, propriétaire du compte hello.

Il existe deux types de comptes de stockage :

* Un compte de stockage standard qui inclut le stockage d’objets blob, de tables, de files d’attente et de fichiers.
* Un compte de stockage Premium prend actuellement en charge uniquement les disques de machine virtuelle Azure. Pour une présentation détaillée de Premium Storage, consultez [Premium Storage : stockage hautes performances pour les charges de travail des machines virtuelles Azure](storage-premium-storage.md) .

## <a name="storage-account-billing"></a>Facturation du compte de stockage
La facturation de l’utilisation d’Azure Storage est basée sur votre compte de stockage. Les coûts de stockage sont basés sur quatre facteurs : la capacité de stockage, le schéma de réplication, les transactions de stockage et l’acheminement des données.

* Capacité de stockage fait référence toohow beaucoup de votre unité de compte de stockage, vous utilisez des données de toostore. coût Hello simplement stocker vos données est déterminée par la quantité de données que vous stockez et comment elle est répliquée.
* La réplication détermine le nombre de copies de vos données qui sont conservées simultanément et à quels emplacements.
* Les transactions font référence tooall lecture et écriture operations tooAzure stockage.
* Sortie de données fait référence toodata transféré à partir d’une région Azure. Lorsque les données hello dans votre compte de stockage sont accessibles par une application qui n’est pas en cours d’exécution dans hello même région, si que l’application est un service cloud ou un autre type d’application, puis vous êtes facturé pour la sortie des données. (Pour des services Azure, vous pouvez effectuer les étapes toogroup vos données et les services Bonjour mêmes données centres tooreduce ou éliminer les frais de sortie de données.)  

Hello [tarification du stockage Azure](https://azure.microsoft.com/pricing/details/storage) page fournit des informations de tarification détaillées pour les transactions, la réplication et la capacité de stockage. Hello [détails de tarification des transferts de données](https://azure.microsoft.com/pricing/details/data-transfers/) page fournit des informations de tarification détaillées pour la sortie de données.

Pour plus d’informations sur la capacité et les objectifs de performance du compte de stockage, consultez la page [Objectifs de performance et évolutivité d’Azure Storage](storage-scalability-targets.md).

> [!NOTE]
> Lorsque vous créez une machine virtuelle Azure, un compte de stockage est créé pour vous automatiquement dans l’emplacement de déploiement hello si vous n’avez pas déjà un compte de stockage à cet emplacement. Par conséquent, il n’est pas nécessaire toofollow les étapes de hello ci-dessous toocreate un compte de stockage pour vos disques de machine virtuelle. nom de compte de stockage Hello doit reposer sur le nom d’ordinateur virtuel hello. Consultez hello [des Machines virtuelles Azure documentation](https://azure.microsoft.com/documentation/services/virtual-machines/) pour plus d’informations.
> 
> 

## <a name="create-a-storage-account"></a>Créez un compte de stockage.
1. Connectez-vous à toohello [portail classique Azure](https://manage.windowsazure.com).
2. Cliquez sur **nouveau** dans la barre des tâches hello bas hello de page de hello. Sélectionnez **Data Services** | **Stockage**, puis cliquez sur **Création rapide**.
   
    ![NewStorageAccount](./media/storage-create-storage-account-classic-portal/storage_NewStorageAccount.png)
3. Dans **URL**, entrez le nom de votre compte de stockage.
   
   > [!NOTE]
   > Les noms des comptes de stockage doivent comporter entre 3 et 24 caractères, uniquement des lettres minuscules et des chiffres.
   > 
   > Le nom de votre compte de stockage doit être unique dans Azure. Hello portail classique Azure indique si le nom de compte de stockage hello que vous sélectionnez est déjà utilisé.
   > 
   > 
   
    Consultez [points de terminaison de compte stockage](#storage-account-endpoints) ci-dessous pour des détails sur comment le nom de compte de stockage hello sera utilisé tooaddress vos objets dans le stockage Azure.
4. Dans **emplacement/groupe d’affinités**, sélectionnez un emplacement pour votre compte de stockage est de fermer les clients tooyou ou tooyour. Si les données dans votre compte de stockage seront accessible à partir d’un autre service Azure, tels qu’une machine virtuelle Azure ou d’un service cloud, vous souhaiterez tooselect un groupe d’affinités hello liste toogroup à partir de votre compte de stockage Bonjour même centre de données avec d’autres services Azure que vous utilisez tooimprove performances et réduire les coûts.
   
    Notez que vous devez sélectionner un groupe d’affinités lors de la création de votre compte de stockage. Vous ne pouvez pas déplacer un groupe tooan compte existant. Pour plus d’informations sur les groupes d’affinités, consultez [Colocalisation de service avec un groupe d’affinités](#service-co-location-with-an-affinity-group) ci-dessous.
   
   > [!IMPORTANT]
   > toodetermine les emplacements qui sont disponibles pour votre abonnement, vous pouvez appeler hello [liste tous les fournisseurs de ressources](https://msdn.microsoft.com/library/azure/dn790524.aspx) opération. fournisseurs de toolist à partir de PowerShell, appelez [Get-AzureLocation](https://msdn.microsoft.com/library/azure/dn757693.aspx). À partir de .NET, utilisez hello [liste](https://msdn.microsoft.com/library/azure/microsoft.azure.management.resources.provideroperationsextensions.list.aspx) méthode Hello ProviderOperationsExtensions classe.
   > 
   > En outre, pour plus d’informations sur les services disponibles dans votre région, consultez [Régions Azure](https://azure.microsoft.com/regions/#services) .
   > 
   > 
5. Si vous avez plusieurs abonnements Azure, puis hello **abonnement** champ s’affiche. Dans **abonnement**, entrez hello abonnement Azure que vous souhaitez que le compte de stockage toouse hello avec.
6. Dans **réplication**, sélectionnez hello niveau souhaité de réplication pour votre compte de stockage. Hello recommandé de l’option de réplication est la réplication géographique redondante, qui fournit une durabilité maximale pour vos données. Pour plus d’informations sur les options de réplication d’Azure Storage, consultez [Réplication Azure Storage](storage-redundancy.md).
7. Cliquez sur **Create Storage Account**.
   
    Il peut prendre quelques minutes toocreate votre compte de stockage. état de hello toocheck, vous pouvez surveiller les notifications de hello bas hello hello portail classique Azure. Une fois que le compte de stockage hello a été créé, votre compte de stockage a **Online** état et est prêt à être utilisé.

![StoragePage](./media/storage-create-storage-account-classic-portal/Storage_StoragePage.png)

### <a name="storage-account-endpoints"></a>Points de terminaison d’un compte de stockage
Chaque objet que vous stockez dans Azure Storage possède une adresse URL unique. formulaires de nom de compte de stockage Hello hello sous-domaine de cette adresse. Hello combinaison de sous-domaine et nom de domaine, qui est un service de tooeach spécifique, forme un *point de terminaison* pour votre compte de stockage.

Par exemple, si votre compte de stockage nommé *mystorageaccount*, sont des points de terminaison hello par défaut pour votre compte de stockage :

* Service BLOB : http://*mystorageaccount*.blob.core.windows.net
* Service de Table : http://*moncomptedestockage*.table.core.windows.net
* Service de File d’attente : http://*moncomptedestockage*.queue.core.windows.net
* Service de fichiers : http://*mystorageaccount*.file.core.windows.net

Vous pouvez voir les points de terminaison hello pour votre compte de stockage sur le tableau de bord de stockage hello Bonjour [portail classique Azure](https://manage.windowsazure.com) une fois hello compte a été créé.

URL de Hello pour accéder à un objet dans un compte de stockage est créé en ajoutant l’emplacement de l’objet hello dans le point de terminaison toohello hello stockage compte. Par exemple, une adresse d’objet blob peut avoir ce format : http://*moncomptedestockage*.blob.core.windows.net/*monconteneur*/*monobjetblob*.

Vous pouvez également configurer un toouse de nom de domaine personnalisé avec votre compte de stockage. Pour plus d’informations, consultez la page [Configurer un nom de domaine personnalisé pour un point de terminaison Blob Storage](storage-custom-domain-name.md) .

### <a name="service-co-location-with-an-affinity-group"></a>Colocalisation de service avec un groupe d’affinités
Un *groupe d'affinités* est un regroupement géographique de vos services et machines virtuelles Azure avec votre compte de stockage Azure. Un groupe d’affinités peut améliorer les performances du service en recherchant les charges de travail ordinateur Bonjour mêmes données centrer ou près de hello utilisateur ciblé. En outre, aucun facturation frais pour la sortie lorsque les données d’un compte de stockage sont accessible à partir d’un autre service qui fait partie de hello même groupe d’affinités.

> [!NOTE]
> toocreate un groupe d’affinités, ouvrez hello <b>paramètres</b> zone Hello [portail classique Azure](https://manage.windowsazure.com), cliquez sur <b>groupes d’affinités</b>, puis cliquez sur <b>ajouter une groupe d’affinités</b> ou hello <b>ajouter</b> bouton. Vous pouvez également créer et gérer des groupes d’affinités à l’aide de hello API de gestion des services Azure. Pour plus d’informations, consultez <a href="http://msdn.microsoft.com/library/azure/ee460798.aspx">Opérations sur les groupes d’affinités</a>.
> 
> 

## <a name="view-copy-and-regenerate-storage-access-keys"></a>Affichage, copie et régénération de clés d’accès de stockage
Lorsque vous créez un compte de stockage, Azure génère deux clés d’accès stockage 512 bits, qui sont utilisées pour l’authentification lors de l’accès au compte de stockage hello. En fournissant deux clés d’accès de stockage, Azure vous permet de clés de hello tooregenerate avec aucun service de stockage tooyour d’interruption ou le service d’accès toothat.

> [!NOTE]
> Nous vous recommandons d’éviter de partager vos clés d’accès de stockage avec qui que ce soit. toopermit accès toostorage ressources sans vous communiquez vos clés d’accès, vous pouvez utiliser un *signature d’accès partagé*. Une signature d’accès partagé fournit des ressources de tooa d’accès dans votre compte pour un intervalle que vous définissez et avec les autorisations hello que vous spécifiez. Pour plus d’informations, consultez [Utilisation des signatures d’accès partagé (SAP)](storage-dotnet-shared-access-signature-part-1.md) .
> 
> 

Bonjour [portail classique Azure](https://manage.windowsazure.com), utilisez **gérer les clés** sur le tableau de bord hello ou hello **stockage** tooview, copier et régénérer hello stockage touches d’accès rapide qui servent de page tooaccess hello services Blob, Table et file d’attente.

### <a name="copy-a-storage-access-key"></a>Copie d'une clé d'accès de stockage
Vous pouvez utiliser **gérer les clés** toocopy un toouse de clé de l’accès de stockage dans une chaîne de connexion. chaîne de connexion Hello requiert le nom de compte de stockage hello et une clé toouse dans l’authentification. Pour plus d’informations sur la configuration de connexion des chaînes tooaccess services de stockage Azure, consultez [configurer des chaînes de connexion de stockage Azure](storage-configure-connection-string.md).

1. Bonjour [portail classique Azure](https://manage.windowsazure.com), cliquez sur **stockage**, puis cliquez sur nom hello du tableau de bord hello stockage compte tooopen hello.
2. Cliquez sur **Manage Keys**.
   
     **Manage Access Keys** s'affiche.
   
    ![Managekeys](./media/storage-create-storage-account-classic-portal/Storage_ManageKeys.png)
3. toocopy une clé d’accès, texte de la touche hello select. Cliquez ensuite avec le bouton droit, puis cliquez sur **Copier**.

### <a name="regenerate-storage-access-keys"></a>Régénération des clés d'accès de stockage
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
2. Régénérer la clé d’accès primaire hello pour votre compte de stockage. Bonjour [portail classique Azure](https://manage.windowsazure.com), à partir du tableau de bord hello ou hello **configurer** , cliquez sur **gérer les clés**. Cliquez sur **régénérer** sous hello clé d’accès primaire, puis cliquez sur **Oui** tooconfirm que vous souhaitez toogenerate une nouvelle clé.
3. Mettre à jour les chaînes de connexion hello dans votre code tooreference hello nouvelle clé primaire.
4. Régénérer la clé d’accès secondaire hello.

## <a name="delete-a-storage-account"></a>Suppression d'un compte de stockage
tooremove un compte de stockage que vous n’utilisez plus, utilisez **supprimer** sur le tableau de bord hello ou hello **configurer** page. **Supprimer** suppressions hello compte de stockage entière, y compris tous les objets BLOB de hello, les tables et les files d’attente dans le compte de hello.

> [!WARNING]
> Il est toorestore n’est pas possible à un compte de stockage supprimé ou récupérer le contenu hello qu’il contenait avant la suppression. Être tooback que rien souhaité toosave avant de supprimer le compte de hello. Cela est également vrai pour toutes les ressources dans le compte de hello, lorsque vous supprimez un objet blob, table, file d’attente ou un fichier, celui-ci est définitivement supprimé.
> 
> Si votre compte de stockage contient des fichiers de disque dur virtuel pour une machine virtuelle Azure, vous devez supprimer toutes les images et les disques qui sont à l’aide de ces fichiers de disque dur virtuel avant de supprimer le compte de stockage hello. Tout d’abord, arrêtez hello virtual machine s’il est en cours d’exécution, puis supprimez-le. les disques toodelete, accédez à toohello **disques** onglet et supprimer tous les disques il. les images toodelete, accédez à toohello **Images** onglet et supprimer les images qui sont stockées dans le compte de hello.
> 
> 

1. Bonjour [portail classique Azure](https://manage.windowsazure.com), cliquez sur **stockage**.
2. Cliquez n’importe où dans l’entrée de compte de stockage hello, à l’exception du nom de hello, puis cliquez sur **supprimer**.
   
     -Ou-
   
    Cliquez sur nom hello de hello stockage compte tooopen hello du tableau de bord, puis cliquez sur **supprimer**.
3. Cliquez sur **Oui** tooconfirm que vous souhaitez le compte de stockage toodelete hello.

## <a name="next-steps"></a>Étapes suivantes
* toolearn en savoir plus sur le stockage Azure, consultez hello [documentation Azure Storage](https://azure.microsoft.com/documentation/services/storage/).
* Visitez hello [Blog de l’équipe stockage Azure](http://blogs.msdn.com/b/windowsazurestorage/).
* [Transfert de données avec l’utilitaire de ligne de commande AzCopy de hello](storage-use-azcopy.md)

