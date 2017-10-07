---
title: meilleures pratiques de RemoteApp aaaAzure | Documents Microsoft
description: "Meilleures pratiques pour la configuration et l'utilisation d’Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b851865b-bec4-4f29-82c0-7b9770c1a520
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: f4d09ef30816eaebb74b69f26f3242c69ea27591
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-configuring-and-using-azure-remoteapp"></a>Meilleures pratiques pour la configuration et l'utilisation d'Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/12/application-remoting-and-the-cloud/) pour plus d’informations.
> 
> 

Hello informations suivantes peut vous aider à configurer et utiliser Azure RemoteApp productive.

## <a name="connectivity"></a>Connectivité
* Utilisez toujours la dernière version de client hello. L'utilisation de clients plus anciens peut entraîner des problèmes de connectivité et d'autres problèmes d'utilisation. L’activation des mises à jour automatique de l’application pour votre appareil permettra de que cette dernière version du client hello est toujours installé.
* Utilisez toujours hello plus stable et fiable internet connexion disponible tooyou.  
* Utilisez uniquement des connexions proxy prises en charge pour bénéficier de performances de connectivité optimales.  accès au proxy SOCKS Hello n’est pas pris en charge.

## <a name="applications"></a>Applications
* Enregistrez et fermez les applications RemoteApp lorsque vous avez terminé avec l’application hello. Ferme ne pas application hello peut entraîner une perte de données.
* Validez les applications personnalisées avant de les utiliser dans Azure RemoteApp. Cela implique de vérifier qu’ils fonctionnent sur une plateforme de session multiples et n’utilisent pas de ressources inutiles comme la mémoire et du processeur peut priver de temps processeur un autre utilisateur de hello même collection. Pour plus d’informations, téléchargez et lisez les hello [compatibilité meilleures pratiques pour les Services Bureau à distance](http://www.dabcc.com/resources/Application%20Compatibility%20Best%20Practices%20for%20Remote%20Desktop%20Services.pdf).

## <a name="configuration-and-management"></a>Configuration et gestion
* Conservez vos images de modèle des toodate, l’installation des mises à jour logicielles et autres correctifs critiques en fonction des besoins. Cela garantit que la capacité, chaque instance est corrigée comme Azure RemoteApp auto-échelles toomeet.  
* Assurez-vous que votre déploiement de services ADFS est sécurisé et fiable. Sinon, les authentifications client peuvent échouer, empêchant alors les utilisateurs d'accéder à Azure RemoteApp.
* Configurez des images de modèle avec les applications, les rôles ou les fonctionnalités installés de sorte qu'elles soient sans état. Ils ne doivent pas dépendre toutes les instances d’ordinateurs virtuels hello dans un service RemoteApp en cours dans un état permanent.
  * Stocker toutes les données utilisateur dans les profils utilisateur ou autre service de toohello externe emplacements de stockage, tels que local partages de fichiers ou OneDrive.
  * Stocker des données partagées dans le service de stockage d’emplacements externes toohello, comme sur site partages de fichiers ou OneDrive.
  * Configurez les paramètres de l’échelle du système dans l’image de modèle hello plutôt que sur les machines virtuelles dans un service.
  * Désactiver les mises à jour automatiques pour les applications publiées : à la place les appliquer manuellement toohello image du modèle et les tester avant de déployer à partir du modèle de hello.

