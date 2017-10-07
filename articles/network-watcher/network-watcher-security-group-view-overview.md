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
# <a name="introduction-toonetwork-security-group-view-in-azure-network-watcher"></a><span data-ttu-id="3e050-103">Affichage du groupe introduction toonetwork sécurité dans l’Observateur réseau de Azure</span><span class="sxs-lookup"><span data-stu-id="3e050-103">Introduction toonetwork security group view in Azure Network Watcher</span></span>

<span data-ttu-id="3e050-104">Les groupes de sécurité réseau sont associés à un niveau de sous-réseau ou à un niveau de carte réseau.</span><span class="sxs-lookup"><span data-stu-id="3e050-104">Network Security groups are associated at a subnet level or at a NIC level.</span></span> <span data-ttu-id="3e050-105">Lorsqu’ils sont associés à un niveau de sous-réseau, elle s’applique des instances de machine virtuelle tooall hello dans un sous-réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="3e050-105">When associated at a subnet level, it applies tooall hello VM instances in hello subnet.</span></span> <span data-ttu-id="3e050-106">Affichage du groupe de sécurité réseau retourne toutes les règles qui sont associés à un niveau de carte réseau et le sous-réseau pour un ordinateur virtuel qui fournit un aperçu de la configuration de hello et les groupes de sécurité réseau hello configuré.</span><span class="sxs-lookup"><span data-stu-id="3e050-106">Network Security Group view returns all hello configured NSGs and rules that are associated at a NIC and subnet level for a virtual machine providing insight into hello configuration.</span></span> <span data-ttu-id="3e050-107">En outre, les règles de sécurité efficace hello sont retournées pour chacune des cartes réseau de hello dans une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3e050-107">In addition, hello effective security rules are returned for each of hello NICs in a VM.</span></span> <span data-ttu-id="3e050-108">L’affichage du groupe de sécurité réseau vous permet de déterminer les vulnérabilités réseau d’une machine virtuelle, telles que les ports ouverts.</span><span class="sxs-lookup"><span data-stu-id="3e050-108">Using Network Security Group view, you can assess a VM for network vulnerabilities such as open ports.</span></span> <span data-ttu-id="3e050-109">Vous pouvez également valider si votre groupe de sécurité réseau fonctionne comme prévu selon un [comparaison entre hello configuré et hello des règles de sécurité efficace](network-watcher-nsg-auditing-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="3e050-109">You can also validate if your Network Security Group is working as expected based on a [comparison between hello configured and hello effective security rules](network-watcher-nsg-auditing-powershell.md).</span></span>

<span data-ttu-id="3e050-110">Un cas d’utilisation plus poussée concerne l’audit et la conformité de la sécurité.</span><span class="sxs-lookup"><span data-stu-id="3e050-110">A more extended use case is in security compliance and auditing.</span></span> <span data-ttu-id="3e050-111">Vous pouvez définir un ensemble normatif de règles de sécurité comme modèle pour la gouvernance de la sécurité de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="3e050-111">You can define a prescriptive set of security rules as a model for security governance in your organization.</span></span> <span data-ttu-id="3e050-112">Un audit de conformité à intervalles réguliers peut être implémenté de façon par programmation en comparant les règles normative de hello avec les règles efficaces hello pour chacune des machines virtuelles de hello dans votre réseau.</span><span class="sxs-lookup"><span data-stu-id="3e050-112">A periodic compliance audit can be implemented in a programmatic way by comparing hello prescriptive rules with hello effective rules for each of hello VMs in your network.</span></span>

<span data-ttu-id="3e050-113">Bonjour portails règles sont divisées en effet, sous-réseau, Interface réseau et par défaut.</span><span class="sxs-lookup"><span data-stu-id="3e050-113">In hello portal rules are divided by Effective, Subnet, Network Interface, and Default.</span></span> <span data-ttu-id="3e050-114">Cela offre une vue simple hello règles appliquées tooa virtuels.</span><span class="sxs-lookup"><span data-stu-id="3e050-114">This provides a simple view into hello rules applied tooa virtual machine.</span></span> <span data-ttu-id="3e050-115">Un bouton de téléchargement est fourni tooeasily télécharger toutes les règles de sécurité hello, quel que soit l’onglet de hello dans un fichier CSV.</span><span class="sxs-lookup"><span data-stu-id="3e050-115">A download button is provided tooeasily download all hello security rules no matter hello tab into a CSV file.</span></span>

![affichage des groupes de sécurité][1]

<span data-ttu-id="3e050-117">Les règles peuvent être sélectionnées et un nouveau panneau ouvre les préfixes tooshow hello groupe de sécurité réseau et de source et de destination.</span><span class="sxs-lookup"><span data-stu-id="3e050-117">Rules can be selected and a new blade opens up tooshow hello Network Security Group and source and destination prefixes.</span></span> <span data-ttu-id="3e050-118">Dans ce panneau vous pouvez naviguer directement ressource du groupe de sécurité réseau toohello.</span><span class="sxs-lookup"><span data-stu-id="3e050-118">From this blade you can navigate directly toohello Network Security Group resource.</span></span>

![exploration][2]

### <a name="next-steps"></a><span data-ttu-id="3e050-120">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3e050-120">Next steps</span></span>

<span data-ttu-id="3e050-121">Découvrez comment tooaudit votre réseau du groupe de sécurité en consultant les paramètres [des paramètres de groupe de sécurité d’Audit réseau avec PowerShell](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="3e050-121">Learn how tooaudit your Network Security Group settings by visiting [Audit Network Security Group settings with PowerShell](network-watcher-nsg-auditing-powershell.md)</span></span>

[1]: ./media/network-watcher-security-group-view-overview/securitygroupview.png
[2]: ./media/network-watcher-security-group-view-overview/figure1.png









