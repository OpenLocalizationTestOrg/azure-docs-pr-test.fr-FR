---
title: "aaaTechnical les conditions préalables requises pour la création d’une image de machine virtuelle pour hello Azure Marketplace | Documents Microsoft"
description: "Comprendre les exigences de hello pour créer et déployer un toohello d’image de machine virtuelle Azure Marketplace pour d’autres toopurchase."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 63c16966-0304-4b17-a715-368a0a5ccb2c
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 04/29/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: fcae4d9e052581e3c1dfe7962e6d50ec31040419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="technical-prerequisites-for-creating-a-virtual-machine-image-for-hello-azure-marketplace"></a>Conditions préalables de techniques pour la création d’une image de machine virtuelle pour hello Azure Marketplace
Processus hello soigneusement avant le début de lire et comprendre où et pourquoi chaque étape est effectuée. Autant que possible, vous devez préparer les informations de votre société et d’autres données, téléchargez les outils nécessaires, ou créer des composants techniques avant de commencer le processus de création offre hello. Cet article devrait vous aider à mieux comprendre ces étapes.  

## <a name="download-needed-tools--applications"></a>Télécharger les outils et applications nécessaires
Vous devez avoir hello prêts avant de commencer le processus de hello des éléments suivants :

* Fonction du système d’exploitation que vous ciblez, installation hello [applets de commande Azure PowerShell](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WindowsAzurePowershellGet.3f.3f.3fnew.appids) ou [outil de l’interface de ligne de commande de Linux](https://go.microsoft.com/fwlink/?LinkId=253472&clcid=0x409) de hello [téléchargements Azure](https://azure.microsoft.com/downloads/) page.
* Installez l’Explorateur de stockage Azure à partir de CodePlex.
* Téléchargez et installez hello outil de Test de Certification pour Azure Certified :
  * [http://go.microsoft.com/fwlink/?LinkID=526913](http://go.microsoft.com/fwlink/?LinkID=526913). Vous avez besoin d’un outil de certification de Windows XP toorun hello. Si vous n’avez pas un ordinateur basé sur Windows est disponible, vous pouvez exécuter l’outil hello à l’aide d’un ordinateur virtuel Windows dans Azure.

## <a name="platforms-supported"></a>Plateformes prises en charge :
Vous pouvez développer des machines virtuelles Azure sur Windows ou Linux. Certains éléments de hello publication--telles que la création d’un Azure compatibles avec disque dur virtuel (VHD)--utiliser les différents outils et étapes selon le système d’exploitation que vous utilisez :  

* Si vous utilisez Linux, consultez toohello « Créer un disque dur virtuel compatible avec Azure (basés sur Linux) » section de hello [guide de publication d’image de machine virtuelle](marketplace-publishing-vm-image-creation.md).
* Si vous utilisez Windows, consultez toohello « Créer un disque dur virtuel compatible avec Azure (basé sur Windows) » section Hello [guide de publication d’image de machine virtuelle](marketplace-publishing-vm-image-creation.md).

> [!NOTE]
> Vous devez accéder à ordinateur Windows tooa à :
> 
> * Exécutez l’outil de validation de certification hello.
> * Créer des URL de signature d’accès de disque dur virtuel partagé de hello pour hello soumission de certification de disque dur virtuel.
> 
> 

## <a name="develop-your-vhd"></a>Développement de votre disque dur virtuel
Vous pouvez développer des disques durs virtuels de Azure dans le cloud de hello ou locale :

* Un développement dans le cloud signifie que toutes les étapes de développement sont effectuées à distance sur un disque dur virtuel résidant sur Azure.
* Un développement local nécessite de télécharger un disque dur virtuel et de le développer dans une infrastructure locale. Bien que cela soit possible, nous ne le recommandons pas. Notez que développement pour Windows ou SQL local nécessite vous clés de licence toohave hello local approprié. Vous ne pouvez pas inclure ou installer SQL Server après la création d'une machine virtuelle. Vous devez également baser votre offre sur une image SQL approuvée à partir de hello portail Azure. Si vous décidez toodevelop localement, vous devez effectuer quelques étapes différemment si vous avez développé dans le cloud de hello. Pour les informations correspondantes, consultez [Création d’une image de machine virtuelle locale](marketplace-publishing-vm-image-creation-on-premise.md).

[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
