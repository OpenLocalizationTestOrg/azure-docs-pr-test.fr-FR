---
title: "Présentation de l’affichage des groupes de sécurité dans Azure Network Watcher | Microsoft Docs"
description: "Cette page fournit une vue d’ensemble de la fonctionnalité d’affichage des groupes de sécurité de Network Watcher."
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
ms.openlocfilehash: 2c581a2d152a6d3f16de8f249e27a426aa9f844f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-network-security-group-view-in-azure-network-watcher"></a><span data-ttu-id="c49fd-103">Présentation de l’affichage des groupes de sécurité réseau dans Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="c49fd-103">Introduction to network security group view in Azure Network Watcher</span></span>

<span data-ttu-id="c49fd-104">Les groupes de sécurité réseau sont associés à un niveau de sous-réseau ou à un niveau de carte réseau.</span><span class="sxs-lookup"><span data-stu-id="c49fd-104">Network Security groups are associated at a subnet level or at a NIC level.</span></span> <span data-ttu-id="c49fd-105">Lorsqu’il est associé à un niveau de sous-réseau, il s’applique à toutes les instances de machine virtuelle du sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="c49fd-105">When associated at a subnet level, it applies to all the VM instances in the subnet.</span></span> <span data-ttu-id="c49fd-106">L’affichage des groupes de sécurité réseau renvoie toutes les règles et tous les groupes de sécurité réseau configurés qui sont associés à un niveau de sous-réseau et de carte réseau pour une machine virtuelle fournissant des informations sur la configuration.</span><span class="sxs-lookup"><span data-stu-id="c49fd-106">Network Security Group view returns all the configured NSGs and rules that are associated at a NIC and subnet level for a virtual machine providing insight into the configuration.</span></span> <span data-ttu-id="c49fd-107">En outre, les règles de sécurité effectives sont renvoyées pour chacune des cartes réseau d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c49fd-107">In addition, the effective security rules are returned for each of the NICs in a VM.</span></span> <span data-ttu-id="c49fd-108">L’affichage du groupe de sécurité réseau vous permet de déterminer les vulnérabilités réseau d’une machine virtuelle, telles que les ports ouverts.</span><span class="sxs-lookup"><span data-stu-id="c49fd-108">Using Network Security Group view, you can assess a VM for network vulnerabilities such as open ports.</span></span> <span data-ttu-id="c49fd-109">Vous pouvez également valider si votre groupe de sécurité réseau fonctionne comme prévu en [comparant les règles de sécurité effectives avec celles configurées](network-watcher-nsg-auditing-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c49fd-109">You can also validate if your Network Security Group is working as expected based on a [comparison between the configured and the effective security rules](network-watcher-nsg-auditing-powershell.md).</span></span>

<span data-ttu-id="c49fd-110">Un cas d’utilisation plus poussée concerne l’audit et la conformité de la sécurité.</span><span class="sxs-lookup"><span data-stu-id="c49fd-110">A more extended use case is in security compliance and auditing.</span></span> <span data-ttu-id="c49fd-111">Vous pouvez définir un ensemble normatif de règles de sécurité comme modèle pour la gouvernance de la sécurité de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="c49fd-111">You can define a prescriptive set of security rules as a model for security governance in your organization.</span></span> <span data-ttu-id="c49fd-112">Un audit de conformité périodique peut être implémenté de façon programmatique en comparant les règles normatives avec les règles effectives pour toutes les machines virtuelles de votre réseau.</span><span class="sxs-lookup"><span data-stu-id="c49fd-112">A periodic compliance audit can be implemented in a programmatic way by comparing the prescriptive rules with the effective rules for each of the VMs in your network.</span></span>

<span data-ttu-id="c49fd-113">Dans le portail, les règles sont divisées en catégories : Effectives, Sous-réseau, Interface réseau et Par défaut.</span><span class="sxs-lookup"><span data-stu-id="c49fd-113">In the portal rules are divided by Effective, Subnet, Network Interface, and Default.</span></span> <span data-ttu-id="c49fd-114">Cela permet de savoir facilement quelles sont les règles appliquées à une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c49fd-114">This provides a simple view into the rules applied to a virtual machine.</span></span> <span data-ttu-id="c49fd-115">Un bouton de téléchargement est fourni pour télécharger simplement toutes les règles de sécurité, quel que soit l’onglet, dans un fichier CSV.</span><span class="sxs-lookup"><span data-stu-id="c49fd-115">A download button is provided to easily download all the security rules no matter the tab into a CSV file.</span></span>

![affichage des groupes de sécurité][1]

<span data-ttu-id="c49fd-117">Les règles peuvent être sélectionnées et un nouveau panneau s’ouvre pour afficher le groupe de sécurité réseau et les préfixes source et de destination.</span><span class="sxs-lookup"><span data-stu-id="c49fd-117">Rules can be selected and a new blade opens up to show the Network Security Group and source and destination prefixes.</span></span> <span data-ttu-id="c49fd-118">Dans ce panneau, vous pouvez naviguer directement vers la ressource de groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="c49fd-118">From this blade you can navigate directly to the Network Security Group resource.</span></span>

![exploration][2]

### <a name="next-steps"></a><span data-ttu-id="c49fd-120">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c49fd-120">Next steps</span></span>

<span data-ttu-id="c49fd-121">Découvrez comment effectuer un audit de vos paramètres de groupe de sécurité réseau en consultant [Automate NSG auditing with Azure Network Watcher Security group view](network-watcher-nsg-auditing-powershell.md) (Automatiser l’audit des groupes de sécurité réseau avec l’affichage des groupes de sécurité réseau Azure Network Watcher)</span><span class="sxs-lookup"><span data-stu-id="c49fd-121">Learn how to audit your Network Security Group settings by visiting [Audit Network Security Group settings with PowerShell](network-watcher-nsg-auditing-powershell.md)</span></span>

[1]: ./media/network-watcher-security-group-view-overview/securitygroupview.png
[2]: ./media/network-watcher-security-group-view-overview/figure1.png









