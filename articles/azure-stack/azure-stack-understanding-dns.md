---
title: aaaUnderstanding DNS dans la pile de Azure | Documents Microsoft
description: "Présentation des fonctionnalités DNS dans Azure Stack"
services: azure-stack
documentationcenter: 
author: ScottNapolitan
manager: darmour
editor: 
ms.assetid: 60f5ac85-be19-49ac-a7c1-f290d682b5de
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 7/10/2017
ms.author: scottnap
ms.openlocfilehash: f60128cf98af8e98ac2bc87172b54132ed06cd8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-idns-for-azure-stack"></a>Présentation d’iDNS pour Azure Stack
================================

noms de domaines internationaux est une fonctionnalité de pile Azure qui vous permet de tooresolve des noms DNS externes (par exemple, http://www.bing.com).
Il vous permet également les noms de réseau virtuel interne tooregister. En procédant ainsi, vous pouvez résoudre des machines virtuelles sur le même réseau virtuel par nom plutôt que par IP adresse, sans avoir tooprovide entrées de serveur DNS personnalisées de hello.

Cette fonctionnalité a toujours été présente dans Azure, mais elle est également disponible dans Windows Server 2016 et Azure Stack.

## <a name="what-does-idns-do"></a>Que fait iDNS ?
Avec les noms de domaines internationaux dans la pile d’Azure, vous obtenez hello suivant des fonctions, sans avoir toospecify entrées de serveur DNS personnalisées.

* Services de résolution de noms DNS partagés pour les charges de travail de locataire.
* Service DNS faisant autorité pour la résolution de noms et d’inscription DNS dans le réseau virtuel hello du client.
* Service DNS récursif pour la résolution de noms Internet à partir de machines virtuelles de locataire. Les clients n’ont plus toospecify DNS entrées tooresolve Internet des noms personnalisés (par exemple, www.bing.com).

Vous pouvez toujours configurer votre propre DNS et utiliser des serveurs DNS personnalisés si vous le souhaitez. Mais maintenant, si vous souhaitez que les noms DNS Internet toobe tooresolve en mesure de simplement et que vous être en mesure de tooconnect tooother machines virtuelles hello même réseau virtuel, vous n’avez pas besoin toospecify quoi que ce soit, et qu’il fonctionnera.

## <a name="what-does-idns-not-do"></a>Que ne fait pas iDNS ?
Les noms de domaines internationaux ne vous autorise pas toodo est de créer un enregistrement DNS pour un nom qui peut être résolu à partir du réseau virtuel de hello en dehors.

Dans Azure, vous pouvez hello en spécifiant une étiquette de nom DNS qui peut être associée à une adresse IP publique. Vous pouvez choisir l’étiquette hello (préfixe), mais Azure choisit suffixe hello, qui est basée sur la région de hello dans lequel vous créez l’adresse IP publique de hello.

![Capture d’écran de l’étiquette de nom DNS](media/azure-stack-understanding-dns-in-tp2/image3.png)

Dans l’image hello ci-dessus, Azure créera un « A » enregistrement dans DNS pour l’étiquette de nom DNS hello spécifié sous la zone de hello **westus.cloudapp.azure.com**. Le suffixe de préfixe et hello un domaine nom complet (FQDN) pouvant être résolu à partir de n’importe où sur l’ensemble de forme hello Internet public.

Azure pile uniquement prend en charge noms de domaines internationaux pour l’inscription du nom interne, donc il ne peut pas hello suivant.

* Créer un enregistrement DNS dans une zone DNS existante hébergée (par exemple, local.azurestack.external).
* Créer une zone DNS (par exemple, Contoso.com).
* Créer un enregistrement dans votre propre zone DNS personnalisée.
* Prend en charge bon hello des noms de domaine.

