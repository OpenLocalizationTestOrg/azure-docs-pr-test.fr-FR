---
title: "aaaAzure chiffrement de Service de stockage pour les données au repos | Documents Microsoft"
description: "Utilisez tooencrypt de fonctionnalité de chiffrement de Service de stockage Azure hello votre stockage d’objets Blob Azure sur le côté du service hello lors du stockage des données de salutation et déchiffrer la récupération des données de hello."
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: edabe3ee-688b-41e0-b34f-613ac9c3fdfd
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: robinsh
ms.openlocfilehash: 304f1c21200f86f2084ce98788b2fc7ca893d1f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-service-encryption-for-data-at-rest"></a>Azure Storage Service Encryption pour les données au repos
Azure Storage Service de chiffrement (SSE) pour les données au repos vous permet de protéger et de protéger vos données toomeet votre engagements de conformité et de sécurité de l’organisation. Avec cette fonctionnalité, Azure Storage chiffre vos toostorage toopersisting préalable de données et déchiffre tooretrieval préalable automatiquement. Hello chiffrement, le déchiffrement et la gestion de clés sont toousers totalement transparent.

Hello sections suivantes fournissent des instructions détaillées sur la fonctionnalités de chiffrement de Service de stockage toouse hello ainsi hello prise en charge des scénarios et des expériences utilisateur.

## <a name="overview"></a>Vue d'ensemble
Le stockage Azure fournit un ensemble complet des fonctionnalités de sécurité qui en permettent aux développeurs de toobuild des applications sécurisées. Les données peuvent être sécurisées en transit entre une application et Azure au moyen du [chiffrement côté client](storage-client-side-encryption.md), de HTTPs ou de SMB 3.0. La fonctionnalité Storage Service Encryption fournit un chiffrement au repos et se charge de la gestion du chiffrement, du déchiffrement et des clés de façon totalement transparente. Toutes les données sont chiffrées à l’aide de 256 bits [chiffrement AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), un des blocs les plus forts de hello chiffrements disponibles.

SSE fonctionne en chiffrant les données de salutation lorsqu’il est écrit tooAzure stockage et peut être utilisé pour le stockage d’objets Blob Azure et de stockage de fichiers. Elle fonctionne pour les éléments suivants de hello :

* Stockage Standard : comptes de stockage à usage général pour les stockages Blob et Fichier et les comptes de stockage Blob
* Stockage Premium 
* Tous les niveaux de redondance (LRS, ZRS, GRS, RA-GRS)
* Comptes de stockage Azure Resource Manager (non Classic) 
* Toutes les régions.

toolearn reportez-vous plus, Forum aux questions toohello.

tooenable ou désactiver le chiffrement de Service de stockage pour un compte de stockage, se connecter à hello [portail Azure](https://portal.azure.com) et sélectionnez un compte de stockage. Panneau de paramètres hello, recherchez hello section Blob Service comme indiqué dans cette capture d’écran et cliquez sur le chiffrement.

![Capture d’écran du portail affichant l’option de chiffrement](./media/storage-service-encryption/image1.png)
<br/>*Figure 1 : Activer SSE pour le service BLOB (étape 1)*

![Capture d’écran du Portail affichant l’option de chiffrement](./media/storage-service-encryption/image3.png)
<br/>*Figure 2 : Activer SSE pour le service Fichier (étape 1)*

Une fois que vous cliquez sur le paramètre de chiffrement hello, vous pouvez activer ou désactiver le chiffrement de Service de stockage.

![Capture d’écran du Portail affichant les propriétés de chiffrement](./media/storage-service-encryption/image2.png)
<br/>*Figure 3 : Activer SSE pour le service Blob et Fichier (étape 2)*

## <a name="encryption-scenarios"></a>Scénarios de chiffrement
Storage Service Encryption peut être activé au niveau d’un compte de stockage. Une fois activée, les clients choisir quels tooencrypt de services. Il prend en charge hello client les scénarios suivants :

* Chiffrement des Stockages Blob et Fichier dans les comptes Resource Manager.
* Chiffrement d’objet Blob et le Service de fichiers dans les comptes de stockage classique une fois migrés tooResource Gestionnaire des comptes de stockage.

SSE a hello limites suivantes :

* Le chiffrement des comptes de stockage classiques n’est pas pris en charge.
* Les données existantes - SSE chiffre uniquement les données nouvellement créées après que hello le chiffrement est activé. Si par exemple vous créez un nouveau compte de stockage du Gestionnaire de ressources, mais ne pas activer le chiffrement, puis vous chargez des objets BLOB ou archivé compte de stockage de toothat de disques durs virtuels et allumez SSE, ces objets BLOB n’est pas chiffrées, sauf si elles sont réécrites ou copiés.
* Prise en charge de Marketplace - activer le chiffrement des ordinateurs virtuels créé à partir hello Marketplace à l’aide de hello [portail Azure](https://portal.azure.com), PowerShell et CLI d’Azure. image de disque dur virtuel de base Hello restera non chiffrée ; Toutefois, des écritures faits une fois hello machine virtuelle a lancé seront chiffrées.
* Les données des tables et des files d’attente ne sont pas chiffrées.

## <a name="getting-started"></a>Mise en route
### <a name="step-1-create-a-new-storage-accountstorage-create-storage-accountmd"></a>Étape 1 : [Créer un compte de stockage](storage-create-storage-account.md).
### <a name="step-2-enable-encryption"></a>Étape 2 : Activer le chiffrement.
Vous pouvez activer le chiffrement à l’aide de hello [portail Azure](https://portal.azure.com).

> [!NOTE]
> Si vous souhaitez tooprogrammatically activer ou désactivez hello chiffrement de Service de stockage sur un compte de stockage, vous pouvez utiliser hello [API REST de fournisseur de ressources de stockage Azure](https://msdn.microsoft.com/library/azure/mt163683.aspx), hello [bibliothèque de Client de fournisseur de ressources de stockage pour .NET](https://msdn.microsoft.com/library/azure/mt131037.aspx), [Azure PowerShell](/powershell/azureps-cmdlets-docs), ou hello [CLI d’Azure](storage-azure-cli.md).
> 
> 

### <a name="step-3-copy-data-toostorage-account"></a>Étape 3 : Copier compte toostorage de données
Si vous activez SSE pour hello service Blob, tous les objets BLOB écrits le compte de stockage toothat seront chiffrées. Tous les objets blob qui se trouvent déjà dans ce compte de stockage ne seront pas chiffrés jusqu’à ce qu’ils soient réécrits. Vous pouvez copier des données de hello tooone de compte de stockage avec SSE chiffré, ou même activer SSE et copier des objets BLOB de hello à partir d’un seul conteneur tooanother toosure est le chiffrement des données précédentes. Vous pouvez l’utiliser des hello suivant tooaccomplish d’outils. Cela est hello même comportement pour le stockage de fichier ainsi.

#### <a name="using-azcopy"></a>Utilisation d’AzCopy
AzCopy est un utilitaire de ligne de commande Windows conçu pour la copie des données tooand à partir du stockage d’objets Blob Microsoft Azure, de fichier et de Table à l’aide de commandes simples avec des performances optimales. Vous pouvez utiliser cette toocopy vos objets BLOB ou des fichiers à partir d’un tooanother de compte de stockage possède SSE activée. 

toolearn plus, visitez [transférer des données avec l’utilitaire de ligne de commande AzCopy de hello](storage-use-azcopy.md).

#### <a name="using-smb"></a>Utilisation de SMB
Stockage de fichiers Azure offre des partages de fichiers dans le cloud hello à l’aide du protocole SMB standard de hello. Vous pouvez monter un partage de fichiers à partir d’un client local ou dans Azure. Une fois monté, les outils tels que Robocopy peuvent être utilisés toocopy fichiers sur tooAzure que les partages de fichiers. Pour plus d’informations, consultez [comment toomount Azure partage de fichiers sur Windows](storage-file-how-to-use-files-windows.md) et [comment toomount fichier Azure partager sur Linux](storage-how-to-use-files-linux.md).


#### <a name="using-hello-storage-client-libraries"></a>À l’aide des bibliothèques clientes de stockage hello
Vous pouvez copier tooand de données objet blob ou un fichier de stockage d’objets blob ou entre des comptes de stockage à l’aide de notre ensemble complet des bibliothèques clientes de stockage, notamment .NET, C++, Java, Android, Node.js, PHP, Python et Ruby.

toolearn plus, visitez notre [prise en main le stockage Blob Azure à l’aide de .NET](storage-dotnet-how-to-use-blobs.md).

#### <a name="using-a-storage-explorer"></a>Utilisation d’un explorateur de stockage
Vous pouvez utiliser un compte de stockage stockage explorer toocreate, charger et télécharger des données, afficher le contenu des objets BLOB et parcourir les répertoires. Vous pouvez utiliser un de ces comptes de stockage tooyour tooupload objets BLOB avec le chiffrement est activé. Avec certains explorateurs de stockage, vous pouvez également copier des données à partir de l’objet blob tooa autre conteneur de stockage existant dans le compte de stockage hello ou un compte de stockage qui a SSE activée.

toolearn plus, visitez [explorateurs de stockage Azure](storage-explorers.md).

### <a name="step-4-query-hello-status-of-hello-encrypted-data"></a>Étape 4 : Données chiffrées de requête d’état hello Hello
Une version mise à jour des bibliothèques de Client de stockage hello a été déployée qui vous permet d’état de hello tooquery d’un objet de toodetermine si elle est chiffrée ou non. Actuellement disponible uniquement pour le Stockage Blob. Prise en charge pour le stockage de fichier est sur la feuille de route hello. 

Bonjour attendant, vous pouvez appeler [obtenir les propriétés de compte](https://msdn.microsoft.com/library/azure/mt163553.aspx) tooverify qui hello compte de stockage a activé le chiffrement ou une vue hello des propriétés de compte de stockage dans hello portail Azure.

## <a name="encryption-and-decryption-workflow"></a>Flux de travail de chiffrement et de déchiffrement
Voici une brève description du flux de travail de chiffrement/déchiffrement hello :

* client de Hello Active le chiffrement sur le compte de stockage hello.
* Lorsque le client de hello écrit nouvelle tooBlob de données (PUT Blob, placez le bloc, PUT Page, placez les fichiers etc.) ou de stockage de fichiers ; chaque écriture est chiffré à l’aide de 256 bits [chiffrement AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), un des blocs les plus forts de hello chiffrements disponibles.
* Lorsque le client de hello a besoin de données tooaccess (GET Blob, etc.), les données sont automatiquement déchiffrées avant de retourner toohello utilisateur.
* Si le chiffrement est désactivé, nouvelle écriture n’est plus chiffrés et les données chiffrées existantes restent chiffrées jusqu'à ce que réécrit par l’utilisateur de hello. Alors que le chiffrement est activé, écrit tooBlob ou stockage de fichier est chiffré. état Hello des données ne modifie pas avec l’utilisateur hello basculer entre l’activation/désactivation du chiffrement pour le compte de stockage hello.
* Toutes les clés de chiffrement sont stockées, chiffrées et gérées par Microsoft.

## <a name="frequently-asked-questions-about-storage-service-encryption-for-data-at-rest"></a>Forum Aux Questions Azure Storage Service Encryption pour les données au repos
**Q : Je possède déjà un compte de stockage classique. Puis-je activer SSE dessus ?**

R : Non. SSE est uniquement pris en charge sur les comptes de stockage Resource Manager.

**Q : Comment chiffrer les données de mon compte de stockage classique ?**

R : vous pouvez créer un nouveau compte de stockage du Gestionnaire de ressources et copiez vos données à l’aide de [AzCopy](storage-use-azcopy.md) à partir de votre compte de stockage classique existante tooyour qui vient d’être gestionnaire de ressources du compte de stockage créé. 

Si vous migrez votre tooa de compte de stockage classique compte de gestionnaire de ressources de stockage, cette opération est instantanée, il change de type hello de votre compte, mais n’affecte pas vos données existantes. Les nouvelles données écrites ne seront chiffrées qu’après l’activation du chiffrement. Pour plus d’informations, consultez [plateforme pris en charge la Migration de ressources IaaS de classique tooResource Manager](https://azure.microsoft.com/blog/iaas-migration-classic-resource-manager/). Notez que cela n’est pris en charge que pour les services Blob et Fichier.

**Q : Je possède déjà un compte de stockage Resource Manager. Puis-je activer SSE dessus ?**

R : Oui, mais seules les nouvelles données écrites seront chiffrées. Il ne revient pas en arrière et chiffre les données qui étaient déjà présentes. Cela n'est pas encore pris en charge pour hello aperçu de stockage de fichier.

**Q : je souhaite que les données actuelles de tooencrypt hello dans un compte de stockage du Gestionnaire de ressources existant ?**

R : Vous pouvez activer SSE à tout moment dans un compte de stockage Resource Manager. Toutefois, les données qui étaient déjà présentes ne seront pas chiffrées. tooencrypt des données existantes, vous pouvez les copier tooanother nom ou un autre conteneur et puis supprimez les versions hello non chiffré.

**Q : J’utilise Stockage Premium. Puis-je utiliser SSE ?**

R : Oui. SSE est pris en charge par le stockage Standard et Premium Storage.  Stockage Premium n’est pas pris en charge pour hello Service de fichiers.

**Q : Si je crée un compte de stockage et que j’active SSE, puis que je crée une machine virtuelle à l’aide de ce compte de stockage, cela signifie-t-il que ma machine virtuelle est chiffrée ?**

R. : Oui. Les disques créés qui utilisent le nouveau compte de stockage hello seront chiffrées, tant qu’ils sont créés une fois SSE est activé. Si hello que machine virtuelle a été créé à l’aide de la Place de marché Azure, image de disque dur virtuel de base hello restera non chiffrée ; Toutefois, des écritures faits une fois hello machine virtuelle a lancé seront chiffrées.

**Q : Puis-je créer des comptes de stockage dans lesquels SSE est activé à l’aide d’Azure PowerShell et de l’interface de ligne de commande Azure ?**

R. : Oui.

**Q : Quel est le coût d’Azure Storage si SSE est activé ?**

R : Aucun coût supplémentaire n’est facturé.

**Q : qui gère les clés de chiffrement hello ?**

R : les clés de hello sont gérées par Microsoft.

**Q : Puis-je utiliser mes propres clés de chiffrement ?**

R : nous travaillons sur la fourniture de fonctionnalités pour les clients toobring leurs propres clés de chiffrement.

**Q : puis-je révoquer les clés de chiffrement toohello accès ?**

R : pas pour l’instant ; Hello clés sont entièrement gérées par Microsoft.

**Q : Est-ce que SSE est activé par défaut lorsque je crée un compte de stockage ?**

R : SSE n’est pas activée par défaut ; Vous pouvez utiliser hello tooenable portail Azure il. Vous pouvez également programmer activer cette fonctionnalité à l’aide de hello API REST de fournisseur de ressource de stockage.

**Q : En quoi est-ce différent d’Azure Disk Encryption ?**

R : cette fonctionnalité est données tooencrypt utilisé dans le stockage d’objets Blob Azure. Hello chiffrement de disque Azure est utilisé tooencrypt des disques du système d’exploitation et des données dans des machines virtuelles IaaS. Pour plus d’informations, consultez notre [guide de sécurité sur Storage](storage-security-guide.md).

**Q : que se passe-t-il si j’activer SSE, puis accédez et activer le chiffrement de disque Azure sur des disques hello ?**

R: Cela fonctionne de façon transparente. Vos données sont chiffrées par les deux méthodes.

**Q : mon compte de stockage est configuré toobe répliquée géo-redondante. Si j’active SSE, ma copie redondante est-elle également chiffrée ?**

R : Oui, toutes les copies hello du compte de stockage sont chiffrées, et toutes les options de redondance – stockage localement redondant (LRS), stockage redondant de Zone (ZRS), stockage géo-redondant (GRS) et le stockage de géo-redondant d’accès en lecture (RA-GRS) – sont pris en charge.

**Q : Je ne peux pas activer le chiffrement sur mon compte de stockage.**

R : S’agit-il d’un compte de stockage Resource Manager ? Les comptes de stockage classiques ne sont pas pris en charge. 

**Q : SSE est-il autorisé uniquement dans des régions spécifiques ?**

R : hello SSE n’est disponible dans toutes les régions pour le stockage d’objets Blob. Veuillez vérifier hello Section disponibilité pour le stockage de fichier. 

**Q : comment contacter une personne si vous rencontrez des problèmes ou que vous souhaitez tooprovide commentaires ?**

R : Veuillez contacter [ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com) pour tous les problèmes connexes tooStorage chiffrement du Service.

## <a name="next-steps"></a>Étapes suivantes
Le stockage Azure fournit un ensemble complet des fonctionnalités de sécurité qui en permettent aux développeurs de toobuild des applications sécurisées. Pour plus d’informations, visitez hello [Guide de sécurité de stockage](storage-security-guide.md).

