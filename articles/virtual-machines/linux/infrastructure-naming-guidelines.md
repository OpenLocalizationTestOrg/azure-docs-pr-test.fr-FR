---
title: infrastructure aaaAzure affectation de noms-Linux | Documents Microsoft
description: "Découvrez hello clé conception et implémentation des recommandations pour l’affectation de noms dans les services d’infrastructure Azure."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 18ee4fb1-8297-49a1-8d3f-097880be67c7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 333146e7b2071e43527a5d7dc2ec02ebfb316eb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-infrastructure-naming-guidelines-for-linux-vms"></a>Instructions de dénomination d’infrastructure Azure pour machines virtuelles Linux 

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

Cet article se concentre sur comment tooapproach les conventions d’affectation de noms pour tous les votre toobuild de ressources Azure différents logique et facilement identifiable définir des ressources dans votre environnement.

## <a name="implementation-guidelines-for-naming-conventions"></a>Instructions d’implémentation pour les conventions d’affectation de noms
Décisions :

* Quelles sont vos conventions d’affectation de noms pour les ressources Azure ?

Tâches :

* Définir un hello affixes toouse dans votre cohérence toomaintain de ressources.
* Définir le compte de stockage noms hello requis pour les toobe global unique.
* Hello document toobe de convention d’affectation de noms utilisé et distribuer tooall parties impliquées tooensure cohérence entre des déploiements.

## <a name="naming-conventions"></a>Conventions d’affectation de noms
Vous devez avoir une convention d’affectation de noms adaptée avant tout processus de création dans Azure. Une convention d’affectation de noms garantit que toutes les ressources hello ont un nom prévisible, ce qui vous aide à faible charge administrative hello associée à la gestion de ces ressources.

Vous pouvez choisir toofollow un ensemble spécifique de conventions d’affectation de noms définies pour votre organisation ou un abonnement Azure spécifique ou un compte. Bien qu’il soit facile pour les personnes au sein des organisations tooestablish règles implicites en règles lorsque vous travaillez avec des ressources Azure, vous devez tooscale en mesure de toobe pour les équipes qui travaillent ensemble dans Azure.

Convenez d’un ensemble de conventions d’affectation de noms en amont. Certains facteurs sont à prendre en compte pour l’ensemble des règles de dénomination.

## <a name="affixes"></a>Affixes
Lorsque vous cherchez toodefine une convention d’affectation de noms, une décision est si apposer de hello est :

* début de Hello du nom de hello (préfixe)
* fin de Hello du nom de hello (suffixe)

Par exemple, voici les deux noms possibles pour un groupe de ressources à l’aide de hello `rg` apposer :

* Rg-WebApp (préfixe)
* WebApp-Rg (suffixe)

Affixes peuvent faire référence à des aspects toodifferent qui décrivent les ressources hello. Hello tableau suivant présente des exemples en général utilisés.

| Aspect | Exemples | Remarques |
|:--- |:--- |:--- |
| Environnement |dev, stg, prod |Selon l’objectif de hello et le nom de chaque environnement. |
| Lieu |usw (West US), use (East US 2) |En fonction de la région de hello du centre de données hello ou une région de hello d’organisation de hello. |
| Composant, service ou produit Azure |Rg pour groupe de ressources, VNet pour réseau virtuel |En fonction du produit hello pour le hello ressource fournit la prise en charge. |
| Rôle |base de données, application, web |En fonction du rôle hello de machine virtuelle de hello. |
| Instance |01, 02, 03, etc. |Pour les ressources possédant plusieurs instances. Par exemple, des serveurs Web à charge équilibrée dans un service cloud. |

Lors de l’établissement des conventions d’affectation de noms, assurez-vous qu’ils clairement l’état qui effectue toouse pour chaque type de ressource et dans quelle position (suffixe vs de préfixe).

## <a name="dates"></a>Dates
Il est souvent important toodetermine hello date de création du nom de hello d’une ressource. Nous vous recommandons de format de date AAAAMMJJ hello. Ce format garantit non seulement hello complète date est enregistrée, mais également que deux ressources dont les noms diffèrent uniquement sur la date de hello sont triés par ordre alphabétique, dans l’ordre chronologique.

## <a name="naming-resources"></a>Ressources d’affectation de noms
Définissez chaque type de ressource dans la convention d’affectation de noms de hello, qui doit avoir des règles qui définissent comment tooassign noms tooeach ressource qui est créé. Ces règles doivent s’appliquer tooall des types de ressources, par exemple :

* Abonnements
* Comptes
* Comptes de stockage
* Réseaux virtuels
* Sous-réseaux
* Groupes à haute disponibilité
* Groupes de ressources
* Machines virtuelles
* Points de terminaison
* groupes de sécurité réseau ;
* contrôleur

tooensure qui hello nom fournit suffisamment ressource toowhich de toodetermine informations qu'elle fait référence, vous devez utiliser des noms descriptifs.

## <a name="computer-names"></a>Noms des ordinateurs
Lorsque vous créez un ordinateur virtuel (VM), Azure nécessite un nom ordinateur virtuel de caractères en too64 qui est utilisé pour le nom de la ressource hello. Azure utilise hello même nom pour le système d’exploitation hello Bonjour machine virtuelle. Toutefois, ces noms ne peuvent pas toujours être hello même.

Si un ordinateur virtuel est créé à partir d’un fichier d’image de disque dur virtuel qui contient déjà un système d’exploitation, nom d’ordinateur virtuel hello dans Azure peut différer hello nom d’ordinateur de système d’exploitation de l’ordinateur virtuel. Cette situation peut ajouter un degré de gestion tooVM des difficultés, nous ne recommandons par conséquent pas. Affecter hello hello de ressource de machine virtuelle Azure même nom en tant que nom de l’ordinateur hello que vous attribuez le système d’exploitation de toohello de cette machine virtuelle.

Nous vous recommandons de ce nom de machine virtuelle Azure hello est hello identique hello sous-jacent du nom d’ordinateur de système d’exploitation.

## <a name="storage-account-names"></a>Noms des comptes de stockage
Cette section ne s’applique pas trop[disques gérés d’Azure](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), comme vous ne créez pas un compte de stockage distinct. Pour les disques non managés, la dénomination des comptes de stockage est régie par des règles spécifiques. Vous ne pouvez utiliser que des lettres minuscules et des chiffres. Pour plus d’informations, consultez la rubrique [Création d’un compte de stockage](../../storage/storage-create-storage-account.md#create-a-storage-account) . En outre, le nom du compte de stockage hello, avec core.windows.net, doit être un nom DNS valide globalement unique. Par exemple, si le compte de stockage hello est appelée mystorageaccount, hello résultant de noms DNS suivants doivent être uniques :

* mystorageaccount.blob.core.windows.net
* mystorageaccount.table.core.windows.net
* mystorageaccount.queue.core.windows.net

## <a name="next-steps"></a>Étapes suivantes
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

