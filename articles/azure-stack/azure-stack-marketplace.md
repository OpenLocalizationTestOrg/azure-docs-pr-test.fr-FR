---
title: "aaaPublish un élément de marketplace personnalisé dans la pile de Azure (opérateur de cloud) | Documents Microsoft"
description: "Comme un opérateur cloud, découvrez comment toopublish un marketplace personnalisé d’élément dans la pile de Azure."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 60871cbb-eed2-433c-a76d-d605c7aec06c
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: erikje
ms.openlocfilehash: e33e1c6574d43ada1c1c85bf77df7d0d191116aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-azure-stack-marketplace-overview"></a>vue d’ensemble de la pile de Azure Marketplace Hello
Hello Marketplace est une collection de services, applications et ressources personnalisés pour la pile de Azure, telles que les réseaux, les ordinateurs virtuels, stockage et ainsi de suite. Les utilisateurs reviennent ici toocreate nouvelles ressources et déploiement de nouvelles applications. Considérez-le comme un catalogue d’achat où les utilisateurs peuvent parcourir et choisissez hello ils les éléments que vous souhaitez toouse. toouse un élément de Marketplace, les utilisateurs doivent s’abonner offre tooan qui accorde l’élément toohello d’accès.

Comme un opérateur cloud, vous décidez quels tooadd éléments (publier) toohello Marketplace. Vous pouvez publier des éléments tels que des bases de données, App Services, et ainsi de suite. Cela les rend visible tooall vos utilisateurs. Vous pouvez publier des éléments personnalisés que vous créez. Vous pouvez également publier des éléments à partir d’une [liste croissante d’éléments de Place de Marché Azure](azure-stack-marketplace-azure-items.md). Lorsque vous publiez un toohello élément Marketplace, les utilisateurs peuvent le voir dans les cinq minutes.

tooopen hello Marketplace, cliquez sur **nouveau**.

![](media/azure-stack-publish-custom-marketplace-item/image1.png)

## <a name="marketplace-items"></a>Éléments du Marketplace
Un élément Place de Marché Azure Stack est un service, une application ou une ressource que vos utilisateurs peuvent télécharger et utiliser. Tous les éléments d’Azure Marketplace de pile est visible tooall vos utilisateurs.

Chaque élément du Marketplace comporte :

* Modèle Azure Resource Manager pour l’approvisionnement de la ressource
* Les métadonnées telles que les chaînes, les icônes et autres supports marketing
* Mise en forme élément hello toodisplay d’informations dans le portail de hello

Chaque élément publié toohello Marketplace utilise un Package de la galerie Azure (azpkg) du format appelée hello. Ajouter des ressources de déploiement ou d’exécution (par exemple, du code, les fichiers zip avec des logiciels ou images de machine virtuelle) tooAzure de pile séparément, pas dans le cadre de hello élément du Marketplace. 

## <a name="next-steps"></a>Étapes suivantes
[Créer et publier un élément de Place de Marché](azure-stack-create-and-publish-marketplace-item.md)

