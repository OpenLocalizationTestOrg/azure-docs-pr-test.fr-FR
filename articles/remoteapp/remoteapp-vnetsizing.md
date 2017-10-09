---
title: "informations aaaSizing pour un réseau virtuel dans Azure RemoteApp | Documents Microsoft"
description: "En savoir plus sur les conditions de l’adressage IP hello pour Azure RemoteApp en cours d’exécution avec un réseau virtuel"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b6e1c4ba-0236-42b2-bced-69353bf211be
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: f98b831af32c41740b258d122b3e18765be08d97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sizing-information-for-a-vnet-in-azure-remoteapp"></a>Informations sur la taille des réseaux virtuels dans Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

Lorsque vous utilisez Azure RemoteApp avec un réseau virtuel (VNET), RemoteApp utilise des adresses IP au sein du sous-réseau de hello. En fonction de l’échelle de hello de votre service RemoteApp, vous devez tooensure que votre sous-réseau possède suffisamment d’adresses IP pour les ordinateurs virtuels de RemoteApp. Bien que ces indications sur la taille ne soient pas parfaites, compte tenu de la manière dont RemoteApp monte ou descend dynamiquement les machines virtuelles au sein d’une collection, celles-ci vous aideront à évaluer votre plage de sous-réseau. Cela est particulièrement important car, une fois qu’un service RemoteApp est placé dans un réseau virtuel, vous ne peut pas augmenter la taille du sous-réseau hello sans supprimer RemoteApp.

Pour chaque collection RemoteApp que vous souhaitez toorun atteint sa capacité maximale, vous devez disposer de 100 adresses IP disponibles. Par exemple, si vous avez une collection RemoteApp dans le plan Standard de hello et que vous souhaitez toohave hello maximum 500 utilisateurs, vous aurez 100 adresses IP dans la collection. De même, vous devez 100 adresses IP pour une collection RemoteApp dans le plan de base hello a 800 utilisateurs. Si vous envisagez de toohave un nombre d’utilisateurs (inférieur à hello maximale), vous pouvez réduire des adresses IP hello nécessaires par collection. spécification de taille minimale de sous-réseau Hello est 30 adresses IP (/ 27).

Passez en revue hello suivant toomake informations que votre réseau virtuel est configuré et fonctionne correctement :

* [Migrer à partir d’un tooan de réseau virtuel personnel réseau virtuel Azure](remoteapp-migratevnet.md)
* [Valider toouse de réseau virtuel Azure hello avec Azure RemoteApp](remoteapp-vnet.md)

