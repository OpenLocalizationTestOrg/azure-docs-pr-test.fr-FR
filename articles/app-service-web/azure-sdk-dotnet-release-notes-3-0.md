---
title: aaaAzure SDK pour .NET 3.0 Notes | Documents Microsoft
description: Notes de publication du kit SDK Azure pour .NET 3.0
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: c83d815b-fc19-4260-821e-7d2a7206dffc
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 03/07/2017
ms.author: juliako
ms.openlocfilehash: 8970b4c9b64de40dc29a33d69006a00ae5e38a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-30-release-notes"></a>Notes de publication du kit SDK Azure pour .NET 3.0

Cette rubrique contient les notes de publication pour la version 3.0 de hello Azure SDK pour .NET.

##<a name="azure-sdk-for-net-30-release-summary"></a>Synthèse de publication du kit SDK Azure pour .NET 3.0

Date de sortie : 07/03/2017
 
Aucune toohello de modifications avec rupture Azure SDK 3.0 n’ont été introduites dans cette version. Il n’existe également aucune tooleverage de mise à niveau si nécessaire ce SDK avec les projets de Service Cloud existants. utilisation de tooallow de hello Azure SDK 3.0 sans nécessiter une mise à niveau, Azure SDK 3.0 installe toohello mêmes répertoires que le kit SDK Azure 2.9. La plupart des composants hello n’a pas changé de version majeure de hello de 2.9, mais à la place uniquement la mise à jour de numéro de build hello.

## <a name="visual-studio-2017-rtw"></a>Visual Studio 2017 RTW

- Cette version de hello Azure SDK pour .NET est intégrée dans Visual Studio 2017, toohello la charge de travail Azure. Tous les outils hello vous devez toodo le développement Azure feront partie de Visual Studio 2017 à l’avenir. Pour Visual Studio 2015 hello SDK seront toujours disponible via WebPI. Maintenant que Visual Studio 2017 a été publié, nous avons interrompu la publication du kit SDK Azure pour .NET pour Visual Studio 2013.

### <a name="azure-diagnostics"></a>Azure Diagnostics

- Tooonly de comportement modifié hello stocker une chaîne de connexion partielle avec clé hello remplacé par un jeton de chaîne de connexion de stockage de diagnostics Services de cloud computing. clé de stockage réel Hello est maintenant stockée dans le dossier du profil utilisateur hello pour son accès peut être contrôlé. Visual Studio lit la clé de stockage hello dans le dossier de profil utilisateur pour le débogage local et le processus de publication. 
- Dans la réponse toohello modification est décrite ci-dessus, Visual Studio Online de l’équipe étendu hello modèle de tâche de déploiement de Services de cloud computing Azure utilisateurs peuvent spécifier la clé de stockage hello pour définir l’extension diagnostics lors de la publication tooAzure dans l’intégration continue et le déploiement.
- Nous nous efforçons de chaîne de connexion sécurisée toostore possibles et la création de jetons pour Azure Diagnostics (WAD), toohelp vous résoudre des problèmes de configuration entre multiprotocole.
 
### <a name="windows-server-2016-virtual-machines"></a>Machines virtuelles Windows Server 2016

- Visual Studio prend désormais en charge le déploiement des Services de Cloud tooOS ordinateurs virtuels de famille 5 (Windows Server 2016). Pour les services cloud existants, vous pouvez modifier votre tootarget paramètres hello nouvelle famille de systèmes d’exploitation. Lors de la création de nouveaux services de cloud, si vous choisissez le service de hello toocreate à l’aide de .net 4.6 ou ultérieure, il prend par défaut hello service toouse 5 de famille du système d’exploitation.  Pour plus d’informations, vous pouvez consulter hello [famille de systèmes d’exploitation invité prend en charge la table](../cloud-services/cloud-services-guestos-update-matrix.md).

### <a name="known-issues"></a>Problèmes connus

- Le kit SDK Azure .NET 3.0 mentionnait un problème survenant lors de la suppression de Visual Studio 2017 dans une configuration côte à côte avec Visual Studio 2015.  Si vous avez hello Azure SDK est installé pour Visual Studio 2015, hello émulateur de stockage Microsoft Azure et l’émulateur de calcul Microsoft Azure seront supprimés si vous désinstallez Visual Studio 2017.  Cela génère une erreur lors de la création et du débogage de projets de services cloud dans Visual Studio 2015. Dans l’ordre toofix ce problème, réinstallez hello Azure SDK à partir de hello Web Platform Installer.  Hello problème sera résolu dans une prochaine mise à jour de Visual Studio 2017.  .

 
### <a name="azure-in-role-cache"></a>In-Role Cache Azure 

- La prise en charge d’Azure In-Role Cache a pris fin le 30 novembre 2016. Pour plus de détails, cliquez [ici](https://azure.microsoft.com/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).




