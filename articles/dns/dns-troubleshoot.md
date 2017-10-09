---
title: "guide de dépannage DNS aaaAzure | Documents Microsoft"
description: "Comment tootroubleshoot commun problèmes avec le système DNS Azure"
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
editor: 
ms.assetid: 95b01dc3-ee69-4575-a259-4227131e4f9c
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/20/2017
ms.author: jonatul
ms.openlocfilehash: 944aa1811c980063f739268cd2c79b647b2754a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-troubleshooting-guide"></a>Guide de résolution des problèmes d’Azure DNS

Cette page fournit des informations de résolution des problèmes pour les questions Azure DNS les plus fréquentes.

Si cette procédure ne résout pas votre problème, vous pouvez également rechercher ou publier votre problème sur notre [forum de support communautaire sur MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork). Vous pouvez également ouvrir une demande de support Azure.


## <a name="i-cant-create-a-dns-zone"></a>Impossible de créer une zone DNS

tooresolve les problèmes courants, essayez une ou plusieurs des hello comme suit :

1.  Hello de révision de l’audit Azure DNS enregistre la raison de l’échec toodetermine hello.
2.  Chaque nom de zone DNS doit être unique au sein de son groupe de ressources. Autrement dit, deux zones DNS avec hello même nom ne peuvent pas partager un groupe de ressources. Essayez d’utiliser un autre nom de zone ou un autre groupe de ressources.
3.  Vous pouvez voir une erreur « Vous avez atteint ou dépassé le nombre maximal de hello de zones dans l’abonnement {id d’abonnement}. » Soit utiliser un autre abonnement Azure, supprimez certaines zones ou contactez le Support Azure tooraise votre limite d’abonnement.
4.  Vous pouvez voir une erreur « zone de hello '{nom de zone}' n’est pas disponible. » Cette erreur signifie que le système DNS Azure était impossible tooallocate des serveurs de noms de cette zone DNS. Essayez d’utiliser un autre nom de zone. Ou bien, si vous êtes propriétaire du nom de domaine hello, contactez le support Azure, ce qui peut allouer des serveurs de noms pour vous.


### <a name="recommended-documents"></a>**Documents recommandés**

[Enregistrements et zones DNS](dns-zones-records.md)
<br>
[Création d’une zone DNS](dns-getstarted-create-dnszone-portal.md)

## <a name="i-cant-create-a-dns-record"></a>Impossible de créer un enregistrement DNS

tooresolve les problèmes courants, essayez une ou plusieurs des hello comme suit :

1.  Hello de révision de l’audit Azure DNS enregistre la raison de l’échec toodetermine hello.
2.  Jeu d’enregistrements hello existe déjà ?  DNS Azure gère les enregistrements à l’aide d’enregistrement *définit*, qui sont la collection hello d’enregistrements de hello même nom et hello même type. Si un enregistrement hello même nom et le type déjà existe, puis tooadd un autre tel enregistrement, vous devez modifier hello enregistrement existant définie.
3.  Vous essayez de toocreate un enregistrement au sommet de zone DNS hello (hello « root » de la zone de hello) ? Si hello convention DNS est donc toouse hello ' @' caractère en tant que nom de l’enregistrement hello. Notez également que les normes DNS hello n’autorisent pas les enregistrements CNAME au sommet de zone hello.
4.  Constatez-vous un conflit d’enregistrement CNAME ?  les normes DNS Hello ne permettent pas d’un enregistrement CNAME avec le même nom qu’un enregistrement d’un autre type de hello. Si vous avez un CNAME existant, création d’un enregistrement avec hello échoue du même nom d’un type différent.  De même, la création d’un enregistrement CNAME échoue si le nom de hello correspond à un enregistrement existant d’un type différent. Supprimer les conflits hello en supprimant les hello autre enregistrement ou choisir un nom de l’autre enregistrement.
5.  Vous avez atteint hello hello nombre limite de jeux d’enregistrements autorisé dans une zone DNS ? Nombre actuel de Hello d’enregistrement définit et hello nombre maximal de jeux d’enregistrements est affiché dans hello portail Azure, sous « Propriétés hello » pour la zone de hello. Si vous avez atteint cette limite, puis supprimez certains jeux d’enregistrements ou contactez le Support Azure tooraise votre limite de jeu d’enregistrements pour cette zone, puis réessayez. 


### <a name="recommended-documents"></a>**Documents recommandés**

[Enregistrements et zones DNS](dns-zones-records.md)
<br>
[Création d’une zone DNS](dns-getstarted-create-dnszone-portal.md)



## <a name="i-cant-resolve-my-dns-record"></a>Impossible de résoudre mon enregistrement DNS

La résolution de noms DNS est un processus en plusieurs étapes. Elle peut échouer pour de nombreuses raisons. Hello étapes suivantes vous aider à identifier pourquoi la résolution DNS échoue pour un enregistrement DNS dans une zone hébergée dans Azure DNS.

1.  Vérifiez que les enregistrements DNS hello ont été configurées correctement dans le système DNS Azure. Passez en revue les enregistrements DNS de hello Bonjour portail Azure, la vérification que le nom de la zone hello, nom de l’enregistrement et type d’enregistrement sont corrects.
2.  Vérifiez que les enregistrements DNS hello résoudre correctement sur les serveurs DNS de Azure hello.
    - Si vous effectuez des requêtes DNS à partir de votre ordinateur local, vous pouvez voir les résultats mis en cache qui ne reflètent l’état actuel de hello hello de serveurs de noms.  En outre, les réseaux d’entreprise utilisent souvent des serveurs proxy DNS, ce qui empêche les requêtes DNS dirigées vers les serveurs de noms toospecific.  tooavoid ces problèmes, utilisez un service de résolution de nom basée sur le web telles que [digwebinterface](http://digwebinterface.com).
    - Être toospecify que des serveurs de nom correct de hello pour votre zone DNS, comme indiqué dans hello portail Azure.
    - Vérifiez que nom DNS de hello est correct (vous avez toospecify hello complet nom, y compris le nom de la zone hello) et le type d’enregistrement hello est correct
3.  Vérifiez que nom de domaine DNS hello a été correctement [délégué des serveurs DNS de Azure toohello](dns-domain-delegation.md). [De nombreux sites web tiers proposent la validation de délégation DNS](https://www.bing.com/search?q=dns+check+tool). Ce test est un *zone* test de délégation, donc vous devez uniquement entrer un nom de zone DNS hello et pas hello enregistrement nom complet.
4.  Une fois terminée hello ci-dessus, votre enregistrement DNS doit maintenant correctement résolues. tooverify, vous pouvez à nouveau utiliser [digwebinterface](http://digwebinterface.com), cette fois à l’aide des paramètres de serveur de nom hello par défaut.


### <a name="recommended-documents"></a>**Documents recommandés**

[Déléguer un tooAzure de domaine DNS](dns-domain-delegation.md)



## <a name="how-do-i-specify-hello-service-and-protocol-for-an-srv-record"></a>Comment spécifier hello « service » et « protocole » pour un enregistrement SRV ?

DNS Azure gère les enregistrements DNS en tant que jeux d’enregistrements : hello ensemble d’enregistrements par hello même nom et hello même type. Pour un jeu d’enregistrements SRV, hello « service » et « protocole » doivent toobe spécifié en tant que partie du nom du jeu d’enregistrements hello. Hello autres paramètres SRV ('priority', « weight », « port » et « cible ») sont spécifiés séparément pour chaque enregistrement dans le jeu d’enregistrements hello.

Exemples de noms d’enregistrement SRV (nom de service « sip », protocole « tcp ») :

- \_SIP. \_tcp (qui crée un enregistrement défini au sommet de zone hello)
- \_sip.\_tcp.sipservice (crée un jeu d’enregistrements nommé « sipservice »)

### <a name="recommended-documents"></a>**Documents recommandés**

[Enregistrements et zones DNS](dns-zones-records.md)
<br>
[Créer des jeux d’enregistrements DNS et les enregistrements à l’aide de hello portail Azure](dns-getstarted-create-recordset-portal.md)
<br>
[Type d’enregistrement SRV (Wikipedia)](https://en.wikipedia.org/wiki/SRV_record)


## <a name="next-steps"></a>Étapes suivantes

* En savoir plus sur les [Enregistrements et zones DNS](dns-zones-records.md)
* toostart à l’aide de DNS Azure, découvrez comment trop[créer une zone DNS](dns-getstarted-create-dnszone-portal.md) et [créer des enregistrements DNS](dns-getstarted-create-recordset-portal.md).
* toomigrate une zone DNS existante, découvrez comment trop[importer et exporter un fichier de zone DNS](dns-import-export.md).

