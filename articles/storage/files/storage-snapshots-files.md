---
title: "Vue d’ensemble des instantanés de partage pour Azure Files (préversion) | Microsoft Docs"
description: "Un instantané de partage est une version en lecture seule d’un partage Azure Files enregistrée à un point dans le temps pour sauvegarder le partage."
services: storage
documentationcenter: .net
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: edabe3ee-688b-41e0-b34f-613ac9c3fdfd
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/17/2018
ms.author: renash
ms.openlocfilehash: c309804f33fc0e5b2091e18dfe5fe3c9849a2709
ms.sourcegitcommit: 2a70752d0987585d480f374c3e2dba0cd5097880
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="overview-of-share-snapshots-for-azure-files-preview"></a>Vue d’ensemble des instantanés de partage pour Azure Files (préversion)
Azure Files vous permet de prendre des instantanés de partages de fichiers. Les instantanés de partage (préversion) capturent l’état d’un partage à ce point dans le temps. Dans cet article, nous décrivons les fonctionnalités fournies par les instantanés de partage et comment vous pouvez en tirer parti dans votre propre cas d’usage.


## <a name="when-to-use-share-snapshots"></a>Quand utiliser les instantanés de partage

### <a name="protection-against-application-error-and-data-corruption"></a>Protection contre l’altération des données et les erreurs d’application

Les applications qui utilisent des partages de fichiers effectuent des opérations telles que l’écriture, la lecture, le stockage, la transmission et le traitement de données. Si une application présente un défaut de configuration ou qu’un bogue involontaire est introduit, cela risque d’entraîner l’altération ou le remplacement accidentel de quelques blocs. Pour vous protéger contre ces scénarios, vous pouvez prendre un instantané de partage avant de déployer le nouveau code d’application. Si le nouveau déploiement introduit un bogue ou une erreur d’application, vous pouvez revenir à une version précédente de vos données sur ce partage de fichiers. 

### <a name="protection-against-accidental-deletions-or-unintended-changes"></a>Protection contre une suppression accidentelle ou une modification involontaire

Supposons que vous travailliez sur un fichier texte dans un partage de fichiers. Une fois le fichier texte fermé, vous ne pouvez plus annuler les modifications apportées. Dans ce cas, vous devez récupérer une version précédente du fichier. Vous pouvez utiliser les instantanés de partage pour récupérer des versions précédentes du fichier s’il est renommé ou supprimé accidentellement.

### <a name="general-backup-purposes"></a>Sauvegarde générale

Après avoir créé un partage de fichiers, vous pouvez régulièrement créer un instantané de ce partage en vue de l’utiliser à des fins de sauvegarde de données. Pris régulièrement, un instantané de partage facilite la conservation de versions antérieures de données à des fins d’audit ou de récupération d’urgence.

## <a name="capabilities"></a>Fonctionnalités

Un instantané de partage est une copie en lecture seule de vos données à un point dans le temps. Vous pouvez créer, supprimer et gérer les instantanés à l’aide de l’API REST. Les mêmes fonctionnalités sont disponibles dans la bibliothèque cliente, l’interface de ligne de commande Azure (Azure CLI) et le portail Azure. 

Vous pouvez afficher les instantanés d’un partage à l’aide de l’API REST et de SMB. Vous pouvez récupérer la liste des versions d’un répertoire ou d’un fichier, ainsi que monter une version spécifique directement en tant que lecteur. 

Une fois créé, un instantané de partage peut être lu, copié ou supprimé, mais pas modifié. Vous ne pouvez pas copier un instantané de partage entier vers un autre compte de stockage. Vous devez effectuer cette opération fichier par fichier à l’aide d’AzCopy ou d’autres mécanismes de copie.

La fonctionnalité d’instantané de partage est fournie au niveau du partage de fichiers. La récupération est fournie au niveau des fichiers individuels pour permettre la restauration de fichiers spécifiques. Vous pouvez restaurer un partage de fichier complet à l’aide de SMB, de l’API REST, du portail, de la bibliothèque cliente ou des outils PowerShell/CLI.

Un instantané d’un partage d’un partage de fichiers est identique au partage de fichiers de base, à ceci près que l’URI du partage présente une valeur **DateTime** à la fin qui indique l’heure à laquelle l’instantané de partage a été pris. Par exemple, si l’URI d’un partage de fichiers est http://storagesample.core.file.windows.net/myshare, l’URI de l’instantané de partage ressemble à ce qui suit :
```
http://storagesample.core.file.windows.net/myshare?snapshot=2011-03-09T01:42:34.9360000Z
```

Les instantanés de partage sont conservés jusqu’à ce qu’ils soient explicitement supprimés. Un instantané de partage ne peut pas être conservé plus longtemps que son partage de fichiers de base. Vous pouvez énumérer les instantanés associés au partage de fichiers de base pour effectuer le suivi de vos instantanés actuels. 

Quand vous créez un instantané d’un partage de fichiers, les fichiers stockés dans les propriétés système du partage sont copiés dans l’instantané de partage avec les mêmes valeurs. Les fichiers de base et les métadonnées du partage de fichiers sont également copiés dans l’instantané de partage, sauf si vous spécifiez des métadonnées distinctes pour l’instantané de partage au moment de sa création.

Pour pouvoir supprimer un partage qui contient des instantanés de partage, vous devez d’abord supprimer l’ensemble de ces instantanés.


## <a name="space-usage"></a>Utilisation de l’espace 

Les instantanés de partage sont incrémentiels par nature. Seules les données qui ont changé depuis le dernier instantané de partage sont enregistrées. Cela réduit le temps nécessaire à la création de l’instantané de partage, ainsi que les coûts de stockage. Toute opération d’écriture sur l’objet ou de mise à jour de métadonnées ou de propriétés est stockée dans l’instantané de partage, car elle est considérée comme du contenu changé. 

Afin d’économiser l’espace, vous pouvez supprimer l’instantané de partage pour la période qui a connu la plus forte évolution.

Bien que les instantanés de partage soient enregistrés de façon incrémentielle, vous ne devez conserver que le dernier instantané de partage pour restaurer le partage. Quand vous supprimez un instantané de partage, seules sont supprimées les données propres à ce dernier. Les instantanés actifs contiennent toutes les informations dont vous avez besoin pour parcourir vos données et les restaurer (à partir du moment où l’instantané de partage a été pris) à l’emplacement d’origine ou à un autre emplacement. Vous pouvez effectuer la restauration au niveau élément.

Les instantanés ne sont pas décomptés de votre limite de partage 5 To. L’espace total occupé par les instantanés de partage n’est pas limité. Les limites de compte de stockage continuent de s’appliquer.

## <a name="limits"></a>limites

Le nombre maximal d’instantanés de partage autorisé par Azure Files s’élève aujourd’hui à 200. Au-delà de 200 instantanés de partage, vous devez supprimer les anciens instantanés pour en créer d’autres. 

Les appels simultanés de création d’instantanés de partage ne sont pas limités. La quantité d’espace utilisable par les instantanés d’un partage de fichiers particulier n’est pas limitée. 

## <a name="copying-data-back-to-a-share-from-share-snapshot"></a>Copie des données vers un partage à partir d’un instantané de partage

Les opérations de copie qui impliquent des fichiers et des instantanés de partage obéissent aux règles suivantes :

Vous pouvez copier des fichiers individuels d’un instantané de partage de fichiers vers son partage de base ou vers un autre emplacement. Vous pouvez restaurer une version antérieure d’un fichier ou restaurer le partage de fichiers complet en effectuant une copie fichier par fichier à partir de l’instantané de partage. L’instantané de partage n’est pas promu vers le partage de base. 

L’instantané de partage reste intact après la copie, mais le partage de fichiers de base est remplacé par une copie des données qui étaient disponibles dans l’instantané de partage. Tous les fichiers restaurés sont considérés comme du contenu changé.

Vous pouvez copier un fichier dans un instantané de partage vers une destination avec un nom différent. Le fichier de destination qui en découle est modifiable et n’est pas un instantané de partage.

Quand un fichier de destination est remplacé par une copie, tous les instantanés de partage associés au fichier de destination d’origine restent intacts.

## <a name="general-best-practices"></a>Bonnes pratiques générales 

Quand vous exécutez l’infrastructure sur Azure, automatisez les sauvegardes pour la récupération de données chaque fois que possible. Les actions automatisées sont plus fiables que les processus manuels, contribuant à améliorer la capacité de récupération et la protection des données. Vous pouvez utiliser l’API REST, le Kit de développement logiciel (SDK) client ou des scripts pour l’automatisation.

Avant de déployer le planificateur d’instantané de partage, étudiez attentivement vos paramètres de fréquence et de rétention des instantanés de partage pour éviter de subir des frais d’instantané de partage inutiles.

Les instantanés de partage assurent uniquement une protection au niveau des fichiers. Ils n’empêchent pas les suppressions accidentelles sur un compte de stockage ou un partage de fichiers. Pour protéger un compte de stockage contre les suppressions accidentelles, vous pouvez verrouiller celui-ci ou le groupe de ressources.

## <a name="next-steps"></a>étapes suivantes
* [Utiliser des instantanés de partage](storage-how-to-use-files-snapshots.md)
* [Forum aux questions sur les instantanés de partage](storage-files-faq.md)

