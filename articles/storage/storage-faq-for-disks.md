---
title: Forum aux questions (FAQ) sur les disques de machine virtuelle Azure IaaS | Microsoft Docs
description: "Forum aux questions sur les disques de machines virtuelles et les disques Premium (gérés et non gérés) Azure IaaS"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: e2a20625-6224-4187-8401-abadc8f1de91
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: 31d0aa67b6ca58b75b432ae94f93ebcf6d730380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-about-azure-iaas-vm-disks-and-managed-and-unmanaged-premium-disks"></a>Forum aux questions sur les disques de machines virtuelles et les disques Premium gérés et non gérés Azure IaaS

Dans cet article, nous étudierons les questions fréquentes relatives à Azure Managed Disks et Azure Stockage Premium.

## <a name="managed-disks"></a>Managed Disks

**Qu’est-ce qu’Azure Managed Disks ?**

Managed Disks est une fonctionnalité qui simplifie la gestion des disques associés aux machines virtuelles Azure IaaS en prenant en charge pour vous la gestion des comptes de stockage. Pour plus d’informations, consultez hello [vue d’ensemble de disques gérés](storage-managed-disks-overview.md).

**Si je crée un disque géré standard à partir d’un disque dur virtuel existant de 80 Go, combien cela me coûte-t-il ?**

Un disque géré standard créé à partir d’un disque dur virtuel de 80 Go est traité comme taille de disque standard disponible suivant hello, qui est un disque S10. Vous êtes facturé en fonction toohello S10 disque tarification. Pour plus d’informations, consultez hello [page de tarification](https://azure.microsoft.com/pricing/details/storage).

**Des frais de transaction s’appliquent-ils aux disques gérés Standard ?**

Oui. Vous êtes facturé pour chaque transaction. Pour plus d’informations, consultez hello [page de tarification](https://azure.microsoft.com/pricing/details/storage).

**Pour un disque géré standard, me seront-elles facturées pour hello de taille réelle des données hello sur le disque de hello ou hello configuré capacité de hello disque ?**

Vous êtes facturé en fonction de la capacité de hello mis en service du disque de hello. Pour plus d’informations, consultez hello [page de tarification](https://azure.microsoft.com/pricing/details/storage).

**En quoi la tarification appliquée aux disques gérés Premium est-elle différente de celle associée aux disques non gérés ?**

Hello tarification des disques premium géré est hello identique à celui des disques premium non managé.

**Puis-je modifier hello stockage type de compte (Standard ou Premium) de mes disques gérés ?**

Oui. Vous pouvez modifier le type de compte de stockage hello vos disques gérés à l’aide de hello portail Azure, PowerShell ou hello CLI d’Azure.

**Existe-t-il un moyen que je puisse copier ou exporter un compte de stockage privé tooa disque géré ?**

Oui. Vous pouvez exporter vos disques gérés à l’aide de hello portail Azure, PowerShell ou hello CLI d’Azure.

**Puis-je utiliser un fichier de disque dur virtuel dans un toocreate de compte de stockage Azure un disque géré avec un autre abonnement ?**

Non.

**Puis-je utiliser un fichier de disque dur virtuel dans un toocreate de compte de stockage Azure un disque géré dans une autre région ?**

Non.

**Existe-t-il des restrictions de mise à l’échelle pour les clients utilisant des disques gérés ?**

Disques gérés élimine les limites de hello associées aux comptes de stockage. Toutefois, nombre de hello de disques gérés par abonnement est limité too2, 000 par défaut. Vous pouvez appeler tooincrease de prise en charge ce nombre.

**Puis-je prendre une capture instantanée incrémentielle d’un disque géré ?**

Non. fonctionnalité de capture instantanée actuelle Hello effectue une copie complète d’un disque géré. Toutefois, nous avons l’intention toosupport création d’instantanés incrémentiels hello futures.

**Les machines virtuelles d’un groupe à haute disponibilité peuvent-elles consister en une combinaison de disques gérés et non gérés ?**

Non. Hello machines virtuelles dans un ensemble de disponibilité doit utiliser tous les disques ou tous les disques non managés. Lorsque vous créez un ensemble de disponibilité, vous pouvez choisir le type de disques souhaité toouse.

**Est l’option par défaut de disques gérés hello Bonjour portail Azure ?**

Pas actuellement, mais il sera fait défaut hello Bonjour futures.

**Est-il possible de créer un disque géré vide ?**

Oui. Vous pouvez tout à fait créer un disque vide. Un disque géré peut être créé indépendamment d’une machine virtuelle, par exemple, sans l’attacher tooa machine virtuelle.

**Quel est le nombre de domaines d’erreur hello pris en charge pour un ensemble de disponibilité qui utilise des disques gérés ?**

En fonction de la région de hello où se trouve le groupe à haute disponibilité hello qui utilise des disques gérés, le nombre de domaines d’erreur hello pris en charge est 2 ou 3.

**Comment est le compte de stockage standard hello pour configurer des diagnostics ?**

Vous configurez un compte de stockage privé pour les diagnostics de machine virtuelle. Bonjour future, nous prévoyons de diagnostics de tooswitch tooManaged ainsi des disques.

**Quel type de prise en charge du contrôle d’accès en fonction du rôle est disponible pour Managed Disks ?**

Managed Disks prend en charge trois rôles principaux par défaut :

* Propriétaire : il dispose d’une liberté totale de gestion et contrôle l’accès
* Contributeur : il dispose d’une liberté totale de gestion, mais ne contrôle pas l’accès
* Lecteur : il peut afficher tous les éléments, mais ne peut y apporter de modifications

**Existe-t-il un moyen que je puisse copier ou exporter un compte de stockage privé tooa disque géré ?**

Vous pouvez obtenir une signature d’accès partagé en lecture seule URI pour hello géré de disque et l’utiliser toocopy hello contenu tooa privé local ou compte de stockage.

**Puis-je créer une copie de mon disque géré ?**

Les clients peuvent prendre un instantané de leurs disques gérés, puis utilisez hello instantané toocreate à un autre disque géré.

**Les disques non gérés sont-ils encore pris en charge ?**

Oui. Nous prenons à la fois en charge les disques gérés et non gérés. Nous vous recommandons d’utiliser des disques gérés pour les nouvelles charges de travail et de migrer vos disques toomanaged de charges de travail en cours.


**Si vous créez un disque de 128 Go et augmentez hello taille too130 Go, sera être facturé pour la taille du disque suivant hello (512 Go) ?**

Oui.

**Puis-je créer des disques gérés disposant du stockage localement redondant, géoredondant ou redondant dans une zone ?**

Actuellement, Azure Managed Disks prend uniquement en charge les disques gérés disposant du stockage localement redondant.

**Puis-je réduire la taille de mes disques gérés ?**

Non. Cette fonctionnalité n’est pas prise en charge pour l’instant. 

**Puis-je modifier propriété de nom d’ordinateur hello lorsque spécialisé (Impossible de créer en utilisant l’outil de préparation système hello ou généralisé) d’exploitation du disque du système est utilisée tooprovision une machine virtuelle ?**

Non. Vous ne pouvez pas mettre à jour propriété de nom d’ordinateur hello. Hello nouvelle machine virtuelle hérite du parent de hello machine virtuelle, ce qui était le disque de système d’exploitation utilisé toocreate hello. 

**Où puis-je trouver exemple Azure Resource Manager modèles toocreate machines virtuelles avec des disques gérés ?**
* [Liste de modèles utilisant des disques gérés](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* https://github.com/chagarw/MDPP

## <a name="managed-disks-and-storage-service-encryption"></a>Managed Disks et Storage Service Encryption 

**Azure Storage Encryption est-il activé par défaut lors de la création d’un disque géré ?**

Oui.

**Qui gère les clés de chiffrement hello ?**

Microsoft gère les clés de chiffrement hello.

**Puis-je désactiver Storage Service Encryption pour mes disques gérés ?**

Non.

**Storage Service Encryption est-il disponible dans toutes les régions ?**

Non. Il est disponible dans toutes les régions hello où disques gérés est disponible. Managed Disks est disponible dans toutes les zones publiques et en Allemagne.

**Comment puis-je savoir si mon disque géré est chiffré ?**

Vous pouvez trouver des temps hello quand un disque géré a été créé à partir de hello portail Azure, hello CLI d’Azure et PowerShell. Si hello est après le 9 juin 2017, votre disque est chiffré. 

**Comment puis-je chiffrer mes disques existants qui ont été créés avant le 10 juin 2017 ?**

À compter du 10 juin 2017, nouvelles données écrites tooexisting géré disques sont automatiquement chiffrées. Nous avons également l’intention tooencrypt les données existantes, et le chiffrement hello aura lieu de façon asynchrone en arrière-plan de hello. Si vous devez chiffrer des données existantes maintenant, créez une copie de votre disque. Les nouveaux disques seront chiffrés.

* [Copier les disques gérés à l’aide de hello CLI d’Azure](https://docs.microsoft.com/en-us/azure/storage/scripts/storage-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription?toc=%2fcli%2fmodule%2ftoc.json)
* [Copier les disques gérés à l’aide de PowerShell](https://docs.microsoft.com/en-us/azure/storage/scripts/storage-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription?toc=%2fcli%2fmodule%2ftoc.json)

**Les instantanés et les images gérés sont-ils chiffrés ?**

Oui. Tous les instantanés et les images gérés créés après le 9 juin 2017 sont automatiquement chiffrés. 

**Puis-je convertir des machines virtuelles avec des disques non managés qui sont trouvent sur des comptes de stockage qui sont ou ont été précédemment chiffrée toomanaged disques ?**

Oui

**Un disque dur virtuel exporté à partir d’un disque géré ou un instantané seront-ils également chiffrés ?**

Non. Mais si vous exportez un tooan de disque dur virtuel chiffrée compte de stockage d’un disque géré chiffrée ou d’instantané, puis il est chiffré. 

## <a name="premium-disks-managed-and-unmanaged"></a>Disques Premium : gérés et non gérés

**Si une machine virtuelle utilise une taille qui prend en charge le stockage Premium, comme DSv2, puis-je joindre des disques de données Standard et Premium ?** 

Oui.

**Puis-je attacher premium et la série de taille de tooa de disques de données standard ne prend pas en charge le stockage Premium, série D, Dv2, G ou F ?**

Non. Vous pouvez joindre uniquement les tooVMs de disques de données standard qui n’utilisent pas une série de taille qui prend en charge le stockage Premium.

**Si je crée un disque de données Premium à partir d’un disque dur virtuel existant de 80 Go, combien cela me coûte-t-il ?**

Un disque de données premium créé à partir d’un disque dur virtuel de 80 Go est traité comme la taille du disque hello premium disponible suivant, qui est un disque P10. Vous êtes facturé en fonction toohello P10 disque tarification.

**Existe-t-il des coûts de transaction toouse stockage Premium ?**

Il existe un coût fixe pour chaque taille de disque. Il s’ajoute aux limites spécifiques d’E/S par seconde et de débit. Hello autres coûts sont la bande passante sortante et la capacité d’instantané, le cas échéant. Pour plus d’informations, consultez hello [page de tarification](https://azure.microsoft.com/pricing/details/storage).

**Quelles sont les limites de hello pour e/s et un débit puis-je obtenir à partir du cache de disque hello ?**

Hello combiné des limites pour le cache disque SSD local pour une série DS 4 000 IOPS par cœur et et 33 Mo par seconde par cœur. Hello série GS offre 5 000 IOPS par cœur et 50 Mo par seconde par cœur.

**Est hello que SSD local pris en charge pour une machine virtuelle de disques gérés ?**

Hello SSD local correspond au stockage temporaire qui est inclus dans une machine virtuelle de disques gérés. Ce stockage temporaire n’occasionne aucun frais supplémentaire. Nous vous recommandons de ne pas utiliser cette toostore SSD local vos données d’application, car il n’est pas rendu persistant dans le stockage d’objets Blob Azure.

**Sont des répercussions sur hello utilisez de découpage sur des disques premium ?**

Il n’est pas inconvénient toohello de découpage sur disques Azure sur soit premium ou standard.

## <a name="new-disk-sizes-managed-and-unmanaged"></a>Nouvelles tailles de disque : gérés et non-gérés

**Quelle est la plus grande taille de disque hello pris en charge pour le système d’exploitation et des disques de données ?**

type de partition de Hello Azure prend en charge pour un disque de système d’exploitation est hello MBR master boot record (). Hello MBR prend en charge une taille de disque jusqu'à too2 to. Hello plus grande taille que Azure prend en charge pour un disque de système d’exploitation est de 2 To. Azure prend en charge jusqu'à to too4 pour les disques de données. 

**Qu’est hello plus grand blob taille de page qui est pris en charge ?**

Hello plus grand blob taille de page Azure prend en charge est de 8 To (8 191 Go). Nous ne prennent en charge les objets BLOB de pages plus de 4 To (4 095 Go) attaché tooa machine virtuelle en tant que données ou disques du système d’exploitation.

**Ai-je besoin toouse une nouvelle version de Windows Azure tools toocreate, attacher, redimensionner et télécharger des disques de taille supérieures à 1 to ?**

Vous n’avez pas besoin tooupgrade votre toocreate outils Azure existant, attacher ou redimensionner des disques de taille supérieures à 1 To. tooupload de fichiers à partir de votre disque dur virtuel local directement tooAzure comme un objet blob de pages ou d’un disque non managé, vous devez toouse ensembles hello plus récente de l’outil :

|Outils Azure      | Versions prises en charge                                |
|-----------------|---------------------------------------------------|
|Azure PowerShell | Numéro de version 4.1.0 : version de juin 2017 ou version ultérieure|
|Azure CLI v1     | Numéro de version 0.10.13 : version de mai 2017 ou version ultérieure|
|AzCopy           | Numéro de version 6.1.0 : version de juin 2017 ou version ultérieure|

prise en charge Hello v2 de CLI d’Azure et d’Azure Storage Explorer sera bientôt disponible. 

**Les tailles de disque P4 et P6 sont-elles prises en charge pour les disques non gérés ou les objets blob de pages ?**

Non. Les tailles de disque P4 (32 Go) et P6 (64 Go) sont prises en charge uniquement pour les disques gérés. La prise en charge des disques non gérés et des objets BLOB de page sera bientôt disponible.

**Si mon premium existant géré disque moins de 64 Go a été créé avant l’activation de disque hello (environ 15 juin 2017), comment est elle facturée ?**

Les disques premium petit existants inférieure à 64 Go continuer toobe facturé en fonction toohello P10 avec la tarification. 

**Comment puis-je changer de niveau de disque hello des disques premium petit inférieur à 64 Go à partir de P10 tooP4 ou P6 ?**

Vous pouvez prendre un instantané de vos disques de petite et créez ensuite un Bonjour de commutateur tooautomatically disque tooP4 de niveau de tarification ou P6 en fonction de la taille de hello configuré. 


## <a name="what-if-my-question-isnt-answered-here"></a>Que dois-je faire si je n’ai pas trouvé de réponse à ma question ici ?

Si votre question n’est pas répertoriée ici, faites-le-nous savoir et nous vous aiderons à trouver une réponse. Vous pouvez poser une question à fin hello de cet article dans les commentaires de hello. tooengage avec l’équipe du stockage Azure hello et autres membres de la Communauté sur cet article, utilisez hello MSDN [forum Azure Storage](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).

toorequest fonctionnalités, envoyez votre toohello demandes et idées [forum de commentaires de stockage Azure](https://feedback.azure.com/forums/217298-storage).
