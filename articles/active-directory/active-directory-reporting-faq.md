---
title: aaaAzure Active Directory Reporting Forum aux questions | Documents Microsoft
description: FAQ sur les rapports Azure Active Directory.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 534da0b1-7858-4167-9986-7a62fbd10439
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: be65a05574ea3b5b190cd02a96b211c571ba70bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-faq"></a>FAQ sur les rapports Azure Active Directory

Cet article inclut elles sonttrop des réponses aux questions (FAQ) sur les rapports d’Azure Active Directory.  
Pour plus d’informations, consultez la page [Rapports Azure Active Directory](active-directory-reporting-azure-portal.md). 

**Q : quelle est la rétention des données pour les journaux d’activité (d’Audit et de connexions) hello Bonjour portail Azure ?** 

**R :** nous fournir 7 jours de données pour nos clients libres et en basculant tooan Azure AD Premium 1 ou une licence Premium 2, vous pouvez accéder aux données pour too30 jours. Pour plus d’informations sur la rétention, consultez la page [Stratégies de rétention des rapports Azure Active Directory](active-directory-reporting-retention.md).

--- 

**Q : combien de temps faut-il jusqu'à ce que je peux voir les données d’activité hello une fois que j’ai terminé ma tâche ?**

**R :** journaux d’activité d’Audit ont une latence comprise entre 15 minutes tooan heure. Les journaux d’activité de connexion ont une latence comprise entre 15 minutes pour la plupart des enregistrements et les heures de too2 pour quelques enregistrements.

---

**Q : dois-je toobe qu'une activité de hello toosee administrateur général établie hello portail Azure ou données tooget via hello API ?**

**R :** Non. Vous pouvez être un **sécurité lecteur**, un **administrateur de la sécurité** ou un **administrateur Global** toosee rapportent des données dans le portail Azure ou en y accédant via hello API.

---

**Q : puis-je obtenir des informations du journal d’activité Office 365 via hello portail Azure ?**

**R :** bien activité d’Office 365 et Azure AD activité journaux partage un grand nombre des ressources d’annuaire hello, si vous souhaitez une vue complète de hello journaux d’activité Office 365, vous devez passer des informations du journal toohello centre d’administration Office 365 tooget Office 365 activité.

---


**Q : qui les API utiliser tooget d’informations sur les journaux d’Office 365 activité ?**

**R :** utilisez Bonjour API de gestion Office 365 tooaccess Bonjour [Office 365 activité se connecte via une API](https://msdn.microsoft.com/office-365/office-365-managment-apis-overview).

---

**Q : Combien d’enregistrements peut-on télécharger à partir du Portail Azure ?**

**R :** que vous pouvez télécharger des enregistrements de too120K de hello portail Azure. Hello enregistrements sont triés par *plus récente* et par défaut, vous obtenez des enregistrements de hello plus récent 120 Ko. 

---

**Q : le nombre d’enregistrements puis-je rechercher parmi les activités de hello API ?**

**R :** vous pouvez interroger les enregistrements de millions de too1 (si vous n’utilisez pas opérateur top hello, qui trie les enregistrement hello plus récente). Si vous utilisez l’opérateur « top » de hello, vous pouvez interroger les enregistrements de too500K. Vous trouverez des exemples de requêtes sur la façon dont toouse hello API ici [ici](active-directory-reporting-api-getting-started.md).

---

**Q : Comment obtenir une licence Premium ?**

**R :** consultez [prise en main d’Azure Active Directory Premium](active-directory-get-started-premium.md) pour un toothis répondre à la question.

---

**Q : Au bout de combien de temps peut-on consulter les données d’activité après avoir obtenu une licence Premium ?**

**R :** si vous avez déjà des données d’activités sous la forme d’une licence gratuite, vous pouvez voir hello des mêmes données. Si vous n’avez pas de données, cela prendra un ou deux jours.

---

**Q : Peut-on voir les données du mois dernier après avoir obtenu une licence Azure AD Premium ?**

**R :** si vous avez récemment échangé version Premium de tooa (y compris une version d’évaluation), vous pouvez voir les données des jours de too7 initialement. Lorsque les données s’accumulent, vous verrez too30 jours.

---

**Q : il existe un événement à risque dans la Protection d’identité, mais je ne vois pas connectez-vous correspondant Bonjour toutes les connexions. Est-ce normal ?**

**R :** Oui, Identity Protection évalue les risques pour tous les flux d’authentification, qu’ils soient interactifs ou non. Toutefois, seul rapport de toutes les connexions affiche hello uniquement les connexions interactives.

---

**Q : Comment puis-je télécharger hello « Utilisateurs avec indicateur risque de » rapport dans le portail Azure ?**

**R :** toodownload d’option hello *utilisateurs marqués pour risque* rapport est bientôt.

---

**Q : Comment puis-je savoir pourquoi une connexion ou un utilisateur a été signalé risquée Bonjour portail Azure ?**

**R :** clients d’édition Premium en savoir plus sur hello sous-jacent risque en cliquant sur utilisateur hello dans « Utilisateurs avec indicateur risque » ou en cliquant sur hello « Risquées connexions ». Clients de l’édition gratuite et de base obtenir les utilisateurs à risque de toosee hello et les connexions sans hello sous-jacente des informations sur les événements de risque.

---

**Q : comment les adresses IP sont calculées dans les connexions hello et rapport de connexions risquée ??**

**R :** les adresses IP sont émises de manière à ce qu’il n’existe aucune connexion définitive entre une adresse IP et où se trouve physiquement ordinateur hello avec cette adresse. Ceci est compliqué par des facteurs tels que les fournisseurs mobiles et VPN à émettre des adresses IP à partir de pools centrales souvent très éloignés où DISPOSITIF hello est utilisé. Hello ci-dessus, la conversion d’emplacement physique des tooa adresse IP est un meilleur effort basé sur des traces, les données du Registre, les recherches inversées et d’autres informations. 

---
