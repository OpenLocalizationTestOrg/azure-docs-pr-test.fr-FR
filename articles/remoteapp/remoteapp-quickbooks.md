---
title: aaaDeploy QuickBooks dans Azure RemoteApp | Documents Microsoft
description: "Découvrez comment tooshare QuickBooks avec Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: c5d00753-77c0-4f0d-a5df-9451b46a31d3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: c21b1ac311449be2281f9ce157828260e856f55d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-do-you-deploy-quickbooks-in-azure-remoteapp"></a>Comment déployer QuickBooks dans Azure RemoteApp ?
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

Utilisez hello suivant informations tooshare QuickBooks en tant qu’application dans Azure RemoteApp.

Vous pouvez partager QuickBooks 2015 Enterprise avec Azure RemoteApp dans une collection hybride ou de cloud. fichier de l’entreprise Hello doit résider sur un ordinateur virtuel qui exécute le serveur de base de données QuickBooks distinct à partir de serveurs d’Azure RemoteApp hello. Ne stockez jamais de fichier de l’entreprise sur votre image Azure RemoteApp hello - perte de données est attendue cas dans ce. Seul QuickBooks Enterprise prend en charge un fichier QuickBooks hello hébergement sur un partage externe avec le serveur de base de données QuickBooks accessible via une mise en réseau Windows standard.   

> [!IMPORTANT]
> Hello QuickBooks de base de données serveur qui héberge le fichier de l’entreprise hello doit résider sur un ordinateur de virtuel distinct au sein de hello même réseau virtuel en tant que hello collection Azure RemoteApp.  
> 
> 

## <a name="steps-toodeploy-quickbooks"></a>Étapes toodeploy QuickBooks
1. Créer une machine virtuelle Azure et installer QuickBooks, serveur de base de données QuickBooks et placer le fichier hello entreprise sur une machine virtuelle Azure.  Assurez-vous que tooproperly configurer des règles de pare-feu.
2. Installer QuickBooks sur un [image personnalisée](remoteapp-imageoptions.md) et créer un [collection Azure RemoteApp](remoteapp-collections.md), cloud ou hybride dans hello exactement le même réseau virtuel où la hello machine virtuelle qui héberge hello serveur de base de données QuickBooks avec fichiers d’entreprise réside. 
3. [Publier](remoteapp-publish.md) QuickBooks application toousers
4. Lancer le client de QuickBooks d’Azure RemoteApp hébergé hello, accédez à l’aide du réseau du serveur de base de données du QuickBooks de hello hébergement toohello machine virtuelle standard de Windows et ouvrir le fichier de l’entreprise hello. 

## <a name="documentation-references"></a>Références de documentation
* QuickBooks - [Configurations prises en charge](http://enterprisesuite.intuit.com/products/enterprise-solutions/technical/#top)
* QuickBooks - [Options de déploiement](http://enterprisesuite.intuit.com/everythingenterprise/launchpad/new-user/)

Vous pouvez également consulter ma présentation Ignite, [notions de base de Microsoft Azure RemoteApp gestion et d’Administration](https://channel9.msdn.com/Events/Ignite/2015/BRK3868) -avançons too1:02:45 tooget toohello QuickBooks partie.

## <a name="deployment-architecture"></a>Architecture de déploiement
![Déploiement de QuickBooks + Azure RemoteApp](./media/remoteapp-quickbooks/ra-quickbooks.png)

