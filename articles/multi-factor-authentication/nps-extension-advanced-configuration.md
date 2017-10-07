---
title: "aaaConfigure hello extension d’Azure MFA NPS | Documents Microsoft"
description: "Après l’installation d’extension NPS hello, utilisez ces étapes de configuration avancées telles que la liste des IP approuvées et remplacement de l’UPN."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: c3aed077b23c95f874861eb00c8e6dca668329c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-configuration-options-for-hello-nps-extension-for-multi-factor-authentication"></a>Configuration des options avancées pour hello extension du serveur NPS pour l’authentification multifacteur

Hello, extension de serveur NPS (Network Policy Server) étend vos fonctionnalités d’Azure multi-Factor Authentication sur le cloud dans votre infrastructure locale. Cet article suppose que vous disposez déjà d’extension hello installée et que vous souhaitez maintenant les tooknow comment toocustomize d’extension hello vous doit. 

## <a name="alternate-login-id"></a>ID de connexion de substitution

Étant donné que hello extension de serveur NPS connecte tooboth vos locaux et le cloud répertoires, vous pouvez rencontrer un problème où les noms de principal d’utilisateur local (UPN) ne correspondent pas les noms hello dans le cloud de hello. toosolve ce problème, utiliser une autre connexion ID. 

Au sein de hello extension du serveur NPS, vous pouvez désigner un toobe d’attribut Active Directory utilisé à la place de hello UPN pour Azure multi-Factor Authentication. Cela permet à vos ressources locales avec la vérification en deux étapes vous tooprotect sans modifier votre UPN local. 

la connexion de remplacement tooconfigure ID, accédez trop`HKLM\SOFTWARE\Microsoft\AzureMfa` et modifier hello les valeurs de Registre suivantes :

| Nom | Type | Valeur par défaut | Description |
| ---- | ---- | ------------- | ----------- |
| LDAP_ALTERNATE_LOGINID_ATTRIBUTE | string | Vide | Désigne le nom hello attribut Active Directory que vous souhaitez toouse au lieu de hello UPN. Cet attribut est utilisé en tant qu’attribut de AlternateLoginId hello. Si cette valeur de Registre a la valeur tooa [attribut Active Directory valide](https://msdn.microsoft.com/library/ms675090.aspx) (par exemple, la messagerie ou displayName), puis hello valeur d’attribut est utilisé à la place de UPN l’utilisateur hello pour l’authentification. Si cette valeur de Registre est vide ou non configuré, puis AlternateLoginId est désactivée et l’UPN de l’utilisateur hello est utilisé pour l’authentification. |
| LDAP_FORCE_GLOBAL_CATALOG | booléenne | False | Utilisez cet indicateur tooforce hello de catalogue Global pour les recherches LDAP lorsque vous recherchez AlternateLoginId. Configurer un contrôleur de domaine en tant que catalogue Global, ajoutez hello AlternateLoginId attribut toohello catalogue Global, puis activer cet indicateur. <br><br> Si LDAP_LOOKUP_FORESTS est configuré (n’est pas vide), **cet indicateur est appliqué comme true**, indépendamment de la valeur hello hello du paramètre de Registre. Dans ce cas, hello extension NPS requiert hello toobe de catalogue Global configuré avec l’attribut de AlternateLoginId hello pour chaque forêt. |
| LDAP_LOOKUP_FORESTS | string | Vide | Fournissez une liste séparés par des points-virgules de forêts toosearch. Par exemple, *contoso.com;foobar.com*. Si cette valeur de Registre est configurée, hello extension du serveur NPS recherche itérative dans toutes les forêts hello dans l’ordre de hello dans lequel ils ont été répertoriés et retourne la première valeur AlternateLoginId réussie hello. Si cette valeur de Registre n’est pas configurée, recherche de AlternateLoginId hello est confiné toohello les domaine actuel.|

problèmes tootroubleshoot avec une autre connexion ID, utilisez hello recommande une procédure de [autres erreurs d’ID de connexion](multi-factor-authentication-nps-errors.md#alternate-login-id-errors).

## <a name="ip-exceptions"></a>Exceptions liées aux adresses IP

Si vous avez besoin de disponibilité du serveur toomonitor, comme si les équilibreurs de charge vérifier quels serveurs sont en cours d’exécution avant l’envoi des charges de travail, vous ne souhaitez pas que ces toobe vérifications bloquées par des demandes de vérification. Au lieu de cela, créez une liste d’adresses IP utilisées par les comptes de service, puis désactivez les exigences de l’authentification multifacteur pour cette liste. 

tooconfigure une liste blanche d’adresses IP, accédez trop`HKLM\SOFTWARE\Microsoft\AzureMfa` et configurer hello valeur de Registre suivante : 

| Nom | Type | Valeur par défaut | Description |
| ---- | ---- | ------------- | ----------- |
| IP_WHITELIST | string | Vide | Fournissez une liste séparée par des points-virgules pour les adresses IP. Inclure les adresses IP de hello d’origine des demandes de service, comme hello serveur NAS/VPN des ordinateurs. Les plages d’adresses IP et les sous-réseaux ne sont pas pris en charge. <br><br> Par exemple, *10.0.0.1;10.0.0.2;10.0.0.3*.

Lorsqu’une demande arrive à partir d’une adresse IP qui existe dans la liste verte de hello, vérification en deux étapes est ignorée. adresse IP comparés toohello qui est fourni dans hello est Hello liste blanche d’adresses IP *ratNASIPAddress* attribut de la demande RADIUS hello. Si une demande RADIUS est fourni sans attribut de ratNASIPAddress hello, hello suivant l’avertissement est consigné : « Liste d’autorisation P_WHITE_LIST_WARNING::IP est ignoré car l’adresse IP source est manquant dans la demande RADIUS dans l’attribut de NasIpAddress. »

## <a name="next-steps"></a>Étapes suivantes

[Résoudre les messages d’erreur de hello extension du serveur NPS pour Azure multi-Factor Authentication](multi-factor-authentication-nps-errors.md)
