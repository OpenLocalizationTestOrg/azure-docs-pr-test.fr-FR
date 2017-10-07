---
title: "aaaTroubleshooting Linux VM échecs d’allocation | Documents Microsoft"
description: "Résoudre les problèmes d’allocation pendant la création, le redémarrage ou le redimensionnement d’une machine virtuelle Linux dans Azure"
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue,azure-resourece-manager,azure-service-management
ms.assetid: 1ef41144-6dd6-4a56-b180-9d8b3d05eae7
ms.service: virtual-machines-linux
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2016
ms.author: cjiang
ms.openlocfilehash: 502fbb406b0b4acf086c2586795f69a44cc1a004
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-allocation-failures-when-you-create-restart-or-resize-linux-vms-in-azure"></a>Résoudre les problèmes d’allocation pendant la création, le redémarrage ou le redimensionnement de machines virtuelles Linux dans Azure
Lorsque vous créez une machine virtuelle, redémarrez arrêté de machines virtuelles (désallouées) ou redimensionnez une machine virtuelle, Microsoft Azure alloue des ressources de calcul tooyour abonnement. Vous pouvez parfois recevoir des erreurs lorsque vous effectuez ces opérations--avant même que vous atteigniez les limites d’abonnement Azure hello. Cet article explique les causes hello de certaines hello courants d’échecs d’allocation et suggère des corrections possibles. Hello informations peuvent également être utiles lorsque vous planifiez le déploiement de hello de vos services. Vous pouvez également [résoudre les problèmes d’allocation pendant la création, le redémarrage ou le redimensionnement de machines virtuelles Linux dans Azure](../windows/allocation-failure.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

[!INCLUDE [virtual-machines-common-allocation-failure](../../../includes/virtual-machines-common-allocation-failure.md)]

