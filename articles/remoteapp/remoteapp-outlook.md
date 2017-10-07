---
title: aaaUsing Outlook dans Azure RemoteApp | Documents Microsoft
description: "Découvrez comment tooconfigure et utiliser Outlook dans Azure RemoteApp | Microsoft Azure"
services: remoteapp
documentationcenter: 
author: pavithir
manager: mbaldwin
ms.assetid: cb2a498f-9539-4522-a874-542114926a61
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 119d2629ac47bd8d20d617985a9b488068aa959f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-microsoft-outlook-in-azure-remoteapp"></a>Utilisation de Microsoft Outlook dans Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

Azure RemoteApp prend en charge Microsoft Outlook O365. En savoir plus sur la façon dont [Office fonctionne dans Azure RemoteApp](remoteapp-officesubscription.md). Il existe quelques paramètres recommandés pour Outlook lors de l’utilisation dans Azure RemoteApp.

## <a name="cached-mode"></a>Mode mis en cache
Le mode mis en cache est une configuration recommandée lorsque vous utilisez Outlook dans Azure RemoteApp. Lorsque vous configurez un toouse de compte Outlook 2013 Mode Exchange mis en cache, Outlook 2013 fonctionne à partir d’une copie locale de la boîte aux lettres Microsoft Exchange de l’utilisateur hello qui est stocké dans un fichier de données hors connexion (fichier OST) hello ordinateur de l’utilisateur, ainsi que de hello carnet d’adresses en mode hors connexion (EN MODE HORS CONNEXION). boîte aux lettres de la mise en cache Hello et en mode hors connexion sont régulièrement mises à jour à partir de hello service O365. En savoir plus sur [hello les différences entre le mode de mise en cache et en ligne](https://technet.microsoft.com/library/jj683103.aspx).

Hello utilisateur peut sélectionner **Mode Exchange de mise en cache** ou **Mode en ligne** pendant l’installation de compte ou en modifiant les paramètres de compte hello. Vous pouvez également déployer un mode ou hello autres à l’aide de hello outil de personnalisation Office (OCT) ou de la stratégie de groupe.  

Lisez [des instructions étape par étape sur l’activation du mode mis en cache](https://technet.microsoft.com/library/c6f4cad9-c918-420e-bab3-8b49e1885034#proc).

## <a name="search"></a>Search
Dans Azure RemoteApp, l’utilisation de la recherche dans Outlook présente des limites. Azure RemoteApp utilise des sessions utilisateur tooaccommodate machines virtuelles regroupées. L’indexation de recherche dépend des ID d’ordinateur hello, qui est différent pour les différentes machines virtuelles. Il est possible que chaque fois qu’un utilisateur se connecte à Azure RemoteApp, ils sont suggéré tooa nouvelle machine virtuelle. Cela équivaudrait, si nous activer la recherche locale, indexeur de hello s’exécute chaque fois que les ID de machine hello change (lorsque hello se trouve sur un ordinateur virtuel différent). Selon la taille de hello Hello. Fichier OST, indexeur de hello pourrait prendre une toocomplete beaucoup de temps et utiliser des ressources nécessaires pour les autres applications. La recherche ne serait pas seulement ralentie, mais elle ne renverrait pas de résultats. À l’aide d’un profil de compte en Mode en ligne serait contourner ce problème, mais les performances risquent d’être affectées en raison de l’absence de toohello d’un cache local (voir hello lien ci-dessus pour plus d’informations sur la différence de hello entre le mode de mise en cache et en ligne). Malheureusement, la recherche indexée/locale ne peut pas être désactivée et la recherche en ligne ne peut pas être activée par défaut dans Outlook 2013.

