---
title: "affichage du groupe aaaIntroduction toosecurity dans l’Observateur réseau de Azure | Documents Microsoft"
description: "Cette page fournit une vue d’ensemble de hello fonctionnalité de vue de sécurité de l’Observateur réseau"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: ad27ab85-9d84-4759-b2b9-e861ef8ea8d8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: c2f6dbbffd0aedbb9db4b69d1758f2e66dd7abb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toonetwork-security-group-view-in-azure-network-watcher"></a>Affichage du groupe introduction toonetwork sécurité dans l’Observateur réseau de Azure

Les groupes de sécurité réseau sont associés à un niveau de sous-réseau ou à un niveau de carte réseau. Lorsqu’ils sont associés à un niveau de sous-réseau, elle s’applique des instances de machine virtuelle tooall hello dans un sous-réseau de hello. Affichage du groupe de sécurité réseau retourne toutes les règles qui sont associés à un niveau de carte réseau et le sous-réseau pour un ordinateur virtuel qui fournit un aperçu de la configuration de hello et les groupes de sécurité réseau hello configuré. En outre, les règles de sécurité efficace hello sont retournées pour chacune des cartes réseau de hello dans une machine virtuelle. L’affichage du groupe de sécurité réseau vous permet de déterminer les vulnérabilités réseau d’une machine virtuelle, telles que les ports ouverts. Vous pouvez également valider si votre groupe de sécurité réseau fonctionne comme prévu selon un [comparaison entre hello configuré et hello des règles de sécurité efficace](network-watcher-nsg-auditing-powershell.md).

Un cas d’utilisation plus poussée concerne l’audit et la conformité de la sécurité. Vous pouvez définir un ensemble normatif de règles de sécurité comme modèle pour la gouvernance de la sécurité de votre organisation. Un audit de conformité à intervalles réguliers peut être implémenté de façon par programmation en comparant les règles normative de hello avec les règles efficaces hello pour chacune des machines virtuelles de hello dans votre réseau.

Bonjour portails règles sont divisées en effet, sous-réseau, Interface réseau et par défaut. Cela offre une vue simple hello règles appliquées tooa virtuels. Un bouton de téléchargement est fourni tooeasily télécharger toutes les règles de sécurité hello, quel que soit l’onglet de hello dans un fichier CSV.

![affichage des groupes de sécurité][1]

Les règles peuvent être sélectionnées et un nouveau panneau ouvre les préfixes tooshow hello groupe de sécurité réseau et de source et de destination. Dans ce panneau vous pouvez naviguer directement ressource du groupe de sécurité réseau toohello.

![exploration][2]

### <a name="next-steps"></a>Étapes suivantes

Découvrez comment tooaudit votre réseau du groupe de sécurité en consultant les paramètres [des paramètres de groupe de sécurité d’Audit réseau avec PowerShell](network-watcher-nsg-auditing-powershell.md)

[1]: ./media/network-watcher-security-group-view-overview/securitygroupview.png
[2]: ./media/network-watcher-security-group-view-overview/figure1.png









