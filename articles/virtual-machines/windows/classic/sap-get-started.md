---
title: aaaUsing SAP sur des machines virtuelles Windows | Documents Microsoft
description: "En savoir plus sur l’utilisation de SAP sur des machines virtuelles Windows dans Microsoft Azure"
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: MSSedusch
manager: timlt
editor: 
tags: azure-service-management
keywords: 
ms.assetid: 1b455be4-c02f-43e3-8d39-c2d5f216e646
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: campaign-page
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 10/04/2016
ms.author: sedusch
ms.openlocfilehash: 6c4d8a066a4a8805668e78e67fd2110f2000ee75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-sap-on-windows-virtual-machines-in-azure"></a>Utilisation de SAP sur des machines virtuelles Windows dans Azure
Le Cloud Computing est un terme couramment utilisé qui prend de plus en plus d’importance dans hello secteur informatique, des petites entreprises, les sociétés toolarge et multinationale. Microsoft Azure est la plateforme de Services de Cloud de Microsoft, qui offre un large éventail de nouvelles possibilités de hello. Maintenant les clients sont des applications d’approvisionner et configurer des toorapidly en mesure d’en tant que Services de cloud computing, afin qu’ils ne sont pas tootechnical limité ou restrictions budgétisation. Au lieu de consacrer du temps et budget à l’infrastructure matérielle, les entreprises peuvent se concentrer sur l’application hello, des processus d’entreprise et ses avantages pour les clients et les utilisateurs.

Avec Microsoft Azure Virtual Machines, Microsoft propose une plateforme IaaS (Infrastructure as a Service) complète. Les applications basées sur SAP NetWeaver sont prises en charge sur Machines virtuelles Azure (IaaS). livres blancs de Hello ci-dessous décrivent comment tooplan implémentez SAP NetWeaver applications basées sur et sur les machines virtuelles Windows Azure. Vous pouvez également implémenter des applications basées sur SAP NetWeaver sur des [machines virtuelles Linux](../../linux/classic/sap-get-started.md).

[!INCLUDE [virtual-machines-common-classic-sap-get-started](../../../../includes/virtual-machines-common-classic-sap-get-started.md)]

## <a name="sap-netweaver-on-azure---ha"></a>SAP NetWeaver sur Azure : haute disponibilité
titre : aaaSAP NetWeaver sur Azure : Clustering des Instances ASCS/SCS SAP à l’aide de Cluster de basculement Windows Server sur Azure avec SIOS DataKeeper

Résumé : « ce document décrit comment tooset de SIOS DataKeeper toouse une configuration à haute disponibilité SAP ASCS/SCS sur Azure. SAP protège les composants à point unique de défaillance tels que SAP ASCS/SCS ou les services de réplication de file d’attente avec des configurations de cluster de basculement Windows Server qui nécessitent des disques partagés. Ces composants SAP sont essentielles pour les fonctionnalités d’un système SAP hello. Par conséquent, les besoins de fonctionnalités de haute disponibilité toobe placer dans placer toomake assurer que ces composants peuvent supporter la défaillance d’un serveur ou une machine virtuelle comme étant effectués avec des configurations de Cluster Windows pour complets et les environnements Hyper-V. À compter d’août 2015 Azure lui-même ne peut pas fournir les disques partagés qui seraient nécessaires pour hello Windows en fonction des configurations hautement disponibles requises pour ces composants SAP critiques. Toutefois aide hello du produit de hello DataKeeper de SIOS, des configurations de Cluster de basculement Windows Server en fonction des besoins pour SAP ASCS/SCS peuvent reposer sur la plateforme Azure IaaS de hello. Ce document décrit une approche étape par étape comment tooinstall une configuration de Cluster de basculement Windows Server avec un disque partagé fourni par SIOS Datakeeper dans Azure. papier de Hello détaille les configurations côté Azure, Windows et SAP hello qui rendent configuration à haute disponibilité hello fonctionnent de manière optimale. Hello papier complète hello Documentation d’Installation SAP et les Notes SAP, qui représentent les ressources principales de hello pour les installations et les déploiements de logiciels SAP sur obtiennent des plateformes.

Mise à jour : août 2015

[Télécharger ce guide maintenant](http://go.microsoft.com/fwlink/?LinkId=613056)

