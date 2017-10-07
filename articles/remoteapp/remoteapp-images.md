---
title: "aaaWhat est dans les images de modèle hello Azure RemoteApp ? | Microsoft Docs"
description: "En savoir plus sur les images de modèle hello inclus avec Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7f8442b2-81da-421e-a453-aa53ba2066b7
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: ea012cec8dc581a8bd4a5a138ce302de19d5c6af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-in-hello-azure-remoteapp-template-images"></a>Nouveautés dans les images de modèle hello Azure RemoteApp ?
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

Votre abonnement Azure RemoteApp comprend trois images de modèle :

* Windows Server 2012
* Microsoft Office 365 ProPlus (abonnement Office 365 requis)
* Microsoft Office Professionnel Plus 2013 (version d'évaluation uniquement)

> [!IMPORTANT]
> Votre abonnement Azure RemoteApp vous permet de qu'accéder logiciel toohello dans les images de hello, avec l’exception hello d’Office 365 ProPlus, ce qui nécessite un abonnement distinct, et Office 2013, qui ne peut pas être utilisé en production. Cela signifie que vous pouvez partager les programmes hello ou applications sur les images de modèle hello avec vos utilisateurs. Par exemple, si vous créez un regroupement qui utilise l’image de Windows Server 2012 R2 hello, vous pouvez publier System Center Endpoint Protection pour tooaccess utilisateurs via RemoteApp.
> 
> Extraire hello [RemoteApp licences détails](remoteapp-licensing.md) pour plus d’informations. Et [à l’aide d’Office avec Azure RemoteApp](remoteapp-o365.md) pourquoi les informations de licence Office.
> 
> 

Continuez votre lecture pour en savoir plus sur ce que contient chaque image.

## <a name="windows-server-2012-r2--hello-vanilla-image"></a>Windows Server 2012 R2 (« hello vanille image »)
Cette image est basée sur le système d’exploitation Microsoft Windows Server 2012 R2 Datacenter et a hello suivantes des rôles et fonctionnalités installés toomeet les exigences de hello pour les images de modèle Azure RemoteApp :

* .NET Framework 4.5, 3.5.1, 3.5
* Expérience utilisateur
* Services de prise en charge de l'écriture manuscrite
* Media Foundation
* Hôte de session Bureau à distance
* Windows PowerShell 4.0
* Windows PowerShell ISE
* Prise en charge WoW64

Cette image a également hello suivant des applications installées :

* Adobe Flash Player
* Microsoft Silverlight
* Microsoft System Center 2012 Endpoint Protection
* Microsoft Windows Media Player

## <a name="microsoft-office-365-proplus-subscription-required"></a>Microsoft Office 365 ProPlus (abonnement requis)
Office 365 est hello plus de l’application demandé, nous avons créé une image « personnalisée » pour vous toowork avec.

Cette image est une extension de l’image de vanille hello et a hello les composants suivants de Microsoft Office 365 ProPlus installé en outre les composants toohello décrits dans l’image de Windows Server 2012 R2 hello :

* Access
* Excel
* Lync
* OneNote
* OneDrive entreprise (Notez que l’agent de synchronisation hello n’est pas prise en charge pour une utilisation avec Azure RemoteApp)
* Outlook
* PowerPoint
* Word
* Outils de vérification linguistique Microsoft Office

image de Hello inclut également Pro de Visio et de Project Professionnel.

Et hello suivant des applications, ainsi :

* SQL Native Client
* Pilote ODBC
* Client d'exploration de données SQL Server
* Client MasterDataServices
* Microsoft Publisher
* PowerQuery
* PowerMap

Toutes les fonctionnalités des applications Office 365 ProPlus sont disponibles uniquement pour les utilisateurs qui disposent d'une offre Office 365 ProPlus. Pour plus d’informations sur l’abonnement de hello Office 365 plans consultez [des plans de services Office 365](http://technet.microsoft.com/library/office-365-plan-options.aspx). Des questions supplémentaires ? Extraire hello [Office 365 + RemoteApp](remoteapp-o365.md) plus d’informations. Consultez également nouvel article de hello, [comment toouse votre abonnement Office 365 avec Azure RemoteApp](remoteapp-officesubscription.md).

Notez que vous devez toolicense Office 365 ProPlus, Visio Professionnel et Project Pro séparément, ils ont chacun leur propre licence.

## <a name="microsoft-office-2013-professional-plus-trial-only"></a>Microsoft Office Professionnel Plus 2013 (version d'évaluation uniquement)
Pendant la période d’évaluation gratuite de hello, vous pouvez tester le service hello avec l’image de hello Office 2013.

Cette image est une extension de l’image de vanille hello et a hello les composants suivants de Microsoft Office 2013 Professionnel Plus installé par ailleurs toohello composants décrits dans l’image de Windows Server 2012 R2 hello :

* Access
* Excel
* Lync
* OneNote
* OneDrive entreprise (Notez que l’agent de synchronisation hello n’est pas prise en charge pour une utilisation avec Azure RemoteApp)
* Outlook
* PowerPoint
* projet
* Visio
* Word
* Outils de vérification linguistique Microsoft Office

> [!IMPORTANT]
> **Informations légales :** cette image n’inclut pas de licence Microsoft Office et *ne peut pas être utilisée en production*. image d’Office 2013 Professionnel Plus Hello est destinée uniquement à des fins d’évaluation. Si vous souhaitez que les applications Office toouse dans Azure RemoteApp pour la production, vous avez besoin d’image de Office 365 ProPlus toouse hello. Pour plus d'informations sur la licence Office, consultez [Utilisation d'Office 365 avec Azure RemoteApp](remoteapp-o365.md)
> 
> 

