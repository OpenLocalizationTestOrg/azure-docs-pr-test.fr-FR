---
title: "échecs d’allocation de machine virtuelle Windows aaaTroubleshooting | Documents Microsoft"
description: "Résoudre les problèmes d’allocation pendant la création, le redémarrage ou le redimensionnement de machines virtuelles Windows dans Azure"
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue,azure-resource-manager,azure-service-management
ms.assetid: bb939e23-77fc-4948-96f7-5037761c30e8
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: cjiang
ms.openlocfilehash: d0cc75ac60d952d8e4310cebc37654dc4f80857f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-allocation-failures-when-you-create-restart-or-resize-windows-vms-in-azure"></a>Résoudre les problèmes d’allocation pendant la création, le redémarrage ou le redimensionnement de machines virtuelles Windows dans Azure
Lorsque vous créez une machine virtuelle, redémarrez arrêté de machines virtuelles (désallouées) ou redimensionnez une machine virtuelle, Microsoft Azure alloue des ressources de calcul tooyour abonnement. Vous pouvez parfois recevoir des erreurs lorsque vous effectuez ces opérations--avant même que vous atteigniez les limites d’abonnement Azure hello. Cet article explique les causes hello de certaines hello courants d’échecs d’allocation et suggère des corrections possibles. Hello informations peuvent également être utiles lorsque vous planifiez le déploiement de hello de vos services. Vous pouvez également [résoudre les problèmes d’allocation pendant la création, le redémarrage ou le redimensionnement de machines virtuelles Linux dans Azure](../linux/allocation-failure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

[!INCLUDE [virtual-machines-common-allocation-failure](../../../includes/virtual-machines-common-allocation-failure.md)]

