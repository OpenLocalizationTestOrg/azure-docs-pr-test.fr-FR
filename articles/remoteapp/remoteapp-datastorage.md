---
title: "aaaNever magasin des données sensibles sur des images personnalisées pour Azure RemoteApp | Documents Microsoft"
description: "En savoir plus sur les recommandations de hello pour le stockage des données dans des images personnalisées dans Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 5a19903b-15f9-49d9-9bc1-ae80f2671aa1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 86a0fea218f8826d6d25f50d3c4c36e368e26fb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="never-store-sensitive-data-on-custom-images"></a>Ne stockez jamais de données sensibles sur des images personnalisées
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

Lorsque vous hébergez votre application dans Azure RemoteApp, hello première étape consiste toocreate une image personnalisée. Nous utilisons ce instances de machine virtuelle toocreate image personnalisée qui font Office de vos applications tooyour utilisateurs. image personnalisée de Hello doit contenir uniquement les applications et les données sensibles ne peuvent être perdues, telles que les bases de données SQL, les fichiers du personnel ou des fichiers de données spéciaux tels que les fichiers d’entreprise QuickBooks. Toutes les données sensibles doivent résider externe tooAzure RemoteApp sur un serveur de fichiers, une autre machine virtuelle Azure, ou dans SQL Azure. image de Hello doit simplement hello application hôte se connecte la source de données toohello et présente les données de hello. Consultez [Configuration requise pour les images Azure RemoteApp](remoteapp-imagereqs.md) pour plus d’informations. 

toounderstand pourquoi vous ne devez pas stocker les données sensibles, vous devez toounderstand fonctionnement d’Azure RemoteApp. Lorsqu’une collection est créée ou mis à jour, coulisses hello plusieurs clones ou des copies de l’image de hello sont créés. Toutes les instances de ces ordinateurs virtuels sont des copies exactes de l’image personnalisée de hello ; Lorsque les utilisateurs lancent des applications qu’ils sont connecté tooone de ces instances de machine virtuelle. Mais hello même instance n’est pas garanti et importe peu, car ils ne sont pas permanentes. Bonjour instances de machine virtuelle hello hébergement des applications sont non persistants et peuvent être détruits ou supprimés en fonction, par exemple, au cours de la mise à jour de la collection. 

Une fois que la collection de hello est configurée et les utilisateurs commencent toohello connexion machines virtuelles, les données utilisateur sont persistantes et protégé, car elle est enregistrée sur le stockage distinct au sein d’un disque dur virtuel que nous appelons un [disque de profil utilisateur (UPD)](remoteapp-upd.md), qui est le profil d’utilisateur hello dans c:\users\<userprofile >. Lorsqu’une application démarre, hello UPD est monté et traité comme un profil utilisateur local par le système d’exploitation de hello. En savoir plus sur la façon dont [Azure RemoteApp enregistre les données et paramètres utilisateur](remoteapp-upd.md).

Exemple de données qui ne doit pas résider dans l’image de hello :

* Données partagées pour les utilisateurs tooaccess
* Base de données SQL ou QuickBooks
* Toutes les données de D:\

Exemple de données qui peut résider dans toobe de profil par défaut hello copié dans UPD chaque utilisateurs :

* Fichiers de configuration par utilisateur
* Scripts que les utilisateurs ont besoin de conserver dans leur UPD

Points clés :

* Ne stockez jamais des données sensibles qui peuvent être perdues sur l’image de hello lors de la création d’une image personnalisée.
* Les données sensibles doivent toujours résider sur un serveur de fichiers distincts, en séparant Azure VM, sur le cloud de hello, toohello externe toujours les instances de machine virtuelle qui héberge vos applications dans Azure RemoteApp. 
* Données utilisateur sont enregistrées et persiste dans le disque de profil utilisateur hello (UPD)

