---
title: "chiffrement de disque aaaApply dans le centre de sécurité Azure | Documents Microsoft"
description: "Ce document vous montre comment tooimplement hello recommandation du centre de sécurité Azure ** appliquer le chiffrement de disque **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 6cc7824a-8d6b-4a5f-ab40-e3bbaebc4a91
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: cd803f1120018c5c86da91186eec1e59d425ede7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="apply-disk-encryption-in-azure-security-center"></a>Appliquer le chiffrement de disque dans Azure Security Center
Azure Security Center vous recommande d’appliquer le chiffrement de disques si vous avez des disques de machines virtuelles Windows ou Linux qui ne sont pas chiffrés à l’aide d’Azure Disk Encryption. Disk Encryption vous permet de chiffrer vos disques de machines virtuelles IaaS Windows et Linux.  Le chiffrement est recommandé pour hello du système d’exploitation et les volumes de données sur votre machine virtuelle.

Chiffrement de disque utilise la norme industrielle de hello [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) la fonctionnalité de Windows et hello [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) fonctionnalité de Linux. Ces fonctionnalités offrent des systèmes d’exploitation et toohelp de chiffrement de données protéger et protéger vos données et répondre à vos sécurité de l’organisation et les engagements de conformité. Chiffrement de disque est intégré à [Azure Key Vault](https://azure.microsoft.com/documentation/services/key-vault/) toohelp vous contrôler et gérer des clés de chiffrement de disque hello et des clés secrètes dans votre abonnement de coffre de clés, tout en garantissant que toutes les données dans les disques de machine virtuelle hello sont chiffrées au repos dans votre [ Le stockage Azure](https://azure.microsoft.com/documentation/services/storage/).

> [!NOTE]
> Prend en charge le chiffrement des disques Azure hello suivant des systèmes de d’exploitation Windows server - Windows Server 2008 R2, Windows Server 2012 et Windows Server 2012 R2. Chiffrement de disque est pris en charge sur hello suivant des systèmes de d’exploitation Linux server - Ubuntu, CentOS, SUSE et SUSE Linux Enterprise Server (SLES).
>
>

## <a name="implement-hello-recommendation"></a>Implémenter la recommandation de hello
1. Bonjour **recommandations** panneau, sélectionnez **appliquer le chiffrement de disque**.
2. Bonjour **appliquer le chiffrement de disque** panneau, vous voyez une liste d’ordinateurs virtuels pour lesquels le chiffrement de disque est recommandé.
3. Suivez toothese de chiffrement tooapply hello instructions machines virtuelles.

![][1]

tooencrypt des Machines virtuelles Azure qui ont été identifiées par le centre de sécurité comme nécessitant le chiffrement, nous vous recommandons de hello comme suit :

* Installez et configurez Azure PowerShell. Cela vous permet de toorun hello PowerShell commandes requis tooset des conditions préalables de hello-tooencrypt requis des Machines virtuelles Azure.
* Obtenir et exécuter hello Azure disque chiffrement conditions préalables script Azure PowerShell.
* Chiffrez vos machines virtuelles.

[Chiffrement d’une machine virtuelle Azure](security-center-disk-encryption.md) vous guide à travers ces étapes.  Cette rubrique suppose que vous utilisez Windows 10 en tant qu’ordinateur hello du client à partir de laquelle vous configurez le chiffrement de disque.

Vous pouvez utiliser de nombreuses approches pour les Machines virtuelles Azure. Si vous êtes déjà rompu dans Azure PowerShell ou CLI d’Azure, vous pouvez préférer toouse autres approches. toolearn sur ces autres méthodes, consultez [chiffrement de disque Azure](../security/azure-security-disk-encryption.md).

## <a name="see-also"></a>Voir aussi
Ce document vous a montré comment tooimplement hello centre de sécurité recommandation « appliquer chiffrement de disque. » toolearn en savoir plus sur le chiffrement de disque, voir hello :

* [Chiffrement et gestion de clés avec Azure Key Vault](https://azure.microsoft.com/documentation/videos/azurecon-2015-encryption-and-key-management-with-azure-key-vault/) (vidéo, 36 min 39 s)--Découvrez comment toouse gestion des disques chiffrement pour les machines virtuelles IaaS Azure Key Vault toohelp protéger et de protéger vos données.
* [Chiffrer une Machine virtuelle Azure](security-center-disk-encryption.md) (document)--Découvrez comment tooencrypt des Machines virtuelles Azure.
* [Chiffrement de disque Azure](../security/azure-security-disk-encryption.md) (document)--Découvrez comment tooenable disque chiffrement pour Windows et les machines virtuelles Linux.

toolearn en savoir plus sur le centre de sécurité, voir hello :

* [Définition des stratégies de sécurité dans le centre de sécurité Azure](security-center-policies.md) --Découvrez comment tooconfigure des stratégies de sécurité.
* [Contrôle d’intégrité de la sécurité dans le centre de sécurité Azure](security-center-monitoring.md) --Découvrez comment toomonitor hello d’intégrité de vos ressources Azure.
* [Toosecurity répond et de la gestion des alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md) --Découvrez comment les alertes toosecurity toomanage et y répondre.
* [Gestion des recommandations de sécurité dans Azure Security Center](security-center-recommendations.md) : découvrez comment les recommandations peuvent vous aider à protéger vos ressources Azure.
* [Forum aux questions sur Azure Security Center](security-center-faq.md) --rechercher Forum aux questions sur l’utilisation du service de hello.
* [Blog sur la sécurité Azure](http://blogs.msdn.com/b/azuresecurity/) : recherchez des billets de blog sur la sécurité et la conformité Azure.

<!--Image references-->
[1]: ./media/security-center-apply-disk-encryption/apply-disk-encryption.png
