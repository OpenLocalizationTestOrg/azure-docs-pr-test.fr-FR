---
title: "Audit et journalisation - Outil Microsoft de modélisation des menaces - Azure | Microsoft Docs"
description: "mesures de correction des menaces exposées dans l’outil de modélisation des menaces"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 3f1933fc59862eca7ae6ee40bbd5136e449e5cf1
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="security-frame-auditing-and-logging--mitigations"></a>Infrastructure de sécurité : Audit et journalisation | Corrections 
| Produit/service | Article |
| --------------- | ------- |
| **Dynamics CRM**    | <ul><li>[Identifier les entités sensibles dans votre solution et implémenter l’audit des modifications](#sensitive-entities)</li></ul> |
| **Application web** | <ul><li>[Vérifier que l’audit et la journalisation sont appliqués à l’application](#auditing)</li><li>[Vérifier que la rotation et la séparation des journaux sont en place](#log-rotation)</li><li>[Vérifier que l’application n’enregistre pas de données utilisateur sensibles](#log-sensitive-data)</li><li>[Vérifier que l’accès aux fichiers d’audit et journaux est restreint](#log-restricted-access)</li><li>[Vérifier que les événements de gestion des utilisateurs sont enregistrés](#user-management)</li><li>[Vérifier que le système intègre des défenses contre l’utilisation malveillante](#inbuilt-defenses)</li><li>[Activer la journalisation des diagnostics pour les applications web dans Azure App Service](#diagnostics-logging)</li></ul> |
| **Base de données** | <ul><li>[Vérifier que l’audit des connexions est activé sur SQL Server](#identify-sensitive-entities)</li><li>[Activer la détection des menaces sur SQL Azure](#threat-detection)</li></ul> |
| **Azure Storage** | <ul><li>[Utiliser Azure Storage Analytics pour auditer l’accès d’Azure Storage](#analytics)</li></ul> |
| **WCF** | <ul><li>[Implémenter une journalisation suffisante](#sufficient-logging)</li><li>[Implémenter une gestion suffisante des échecs d’audit](#audit-failure-handling)</li></ul> |
| **API Web** | <ul><li>[Vérifier que l’audit et la journalisation sont appliqués à l’API web](#logging-web-api)</li></ul> |
| **Passerelle de champ IoT** | <ul><li>[Vérifier que l’audit et la journalisation appropriés sont appliqués sur la passerelle de champ](#logging-field-gateway)</li></ul> |
| **Passerelle de cloud IoT** | <ul><li>[Vérifier que l’audit et la journalisation appropriés sont appliqués sur la passerelle de cloud](#logging-cloud-gateway)</li></ul> |

## <a id="sensitive-entities"></a>Identifier les entités sensibles dans votre solution et implémenter l’audit des modifications

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Dynamics CRM | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes**                   | Identifier les entités dans votre solution qui contiennent des données sensibles et implémenter l’audit des modifications sur ces entités et champs |

## <a id="auditing"></a>Vérifier que l’audit et la journalisation sont appliqués à l’application

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes**                   | Activez l’audit et la journalisation sur tous les composants. Les journaux d’audit doivent capturer le contexte de l’utilisateur. Identifiez tous les événements importants et enregistrez ces événements. Implémenter la journalisation centralisée |

## <a id="log-rotation"></a>Vérifier que la rotation et la séparation des journaux sont en place

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes**                   | <p>La rotation des journaux est un processus automatisé utilisé dans l’administration système dans lequel les fichiers journaux obsolètes sont archivés. Les serveurs qui exécutent des applications importantes journalisent généralement chaque demande : en ce qui concerne les journaux volumineux, la rotation des journaux permet de limiter la taille totale des journaux tout en permettant l’analyse des événements récents. </p><p>Par principe, la séparation des journaux signifie que vous devez stocker vos fichiers journaux sur une partition différente de celle sur laquelle votre système d’exploitation/application est exécutée afin d’éviter une attaque par déni de service ou la rétrogradation des performances de votre application</p>|

## <a id="log-sensitive-data"></a>Vérifier que l’application n’enregistre pas de données utilisateur sensibles

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes**                   | <p>Vérifiez que vous n’enregistrez aucune donnée sensible fournie par un utilisateur sur votre site. Vérifiez la journalisation intentionnelle, ainsi que les effets secondaires dus à des problèmes de conception. Voici quelques exemples de données sensibles :</p><ul><li>Informations d’identification de l’utilisateur</li><li>Numéro de sécurité sociale ou autres informations d’identification</li><li>Numéros de carte de crédit ou autres informations financières</li><li>Informations de santé</li><li>Clés privées ou autres données pouvant être utilisées pour déchiffrer des informations chiffrées</li><li>Informations système ou d’application pouvant être utilisées pour attaquer plus efficacement l’application</li></ul>|

## <a id="log-restricted-access"></a>Vérifier que l’accès aux fichiers d’audit et journaux est restreint

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes**                   | <p>Vérifiez que les droits d’accès aux fichiers journaux sont définis correctement. Les comptes d’application doivent disposer d’un accès en écriture seule, et les opérateurs et le personnel de support doit disposer d’un accès en lecture seule en fonction des besoins.</p><p>Les comptes d’administrateur sont les seuls comptes à devoir disposer d’un accès complet. Vérifiez les ACL Windows sur les fichiers journaux pour vous assurer qu’ils sont restreints correctement :</p><ul><li>Les comptes d’application doivent disposer d’accès en écriture seule</li><li>Les opérateurs et le personnel de support doivent disposer d’un accès en lecture seule en fonction des besoins</li><li>Les administrateurs sont les seuls comptes à devoir disposer d’un accès complet</li></ul>|

## <a id="user-management"></a>Vérifier que les événements de gestion des utilisateurs sont enregistrés

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes**                   | <p>Vérifiez que l’application surveille les événements de gestion des utilisateurs tels que les connexions utilisateur ayant réussi ou échoué, les réinitialisations de mot de passe, les modifications de mot de passe, le verrouillage de compte, l’inscription utilisateur. Ceci permet de détecter et de réagir à un comportement potentiellement suspect. Ceci permet également de recueillir des données opérationnelles ; par exemple, pour suivre qui accède à l’application</p>|

## <a id="inbuilt-defenses"></a>Vérifier que le système intègre des défenses contre l’utilisation malveillante

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes**                   | <p>Les contrôles permettant de lever des exceptions de sécurité en cas de mauvaise utilisation de l’application doivent être en place. Par exemple, si la validation des entrées est en place et qu’une personne malveillante tente d’injecter un code malveillant ne correspondant pas à l’expression régulière, une exception de sécurité pouvant être le signe d’une mauvaise utilisation du système peut être relevée</p><p>Par exemple, il est recommandé d’enregistrer des exceptions de sécurité et des actions pour les problèmes suivants :</p><ul><li>Validation des entrées</li><li>Violations CSRF</li><li>Force brute (limite supérieure du nombre de requêtes par utilisateur et par ressource)</li><li>Violations de chargement de fichiers</li><ul>|

## <a id="diagnostics-logging"></a>Activer la journalisation des diagnostics pour les applications web dans Azure App Service

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | EnvironmentType - Azure |
| **Informations de référence**              | N/A  |
| **Étapes** | <p>Azure fournit des diagnostics intégrés pour aider au débogage d'une application web App Service. Ils s’appliquent également aux applications API et aux applications mobiles. Les applications web App Service fournissent des fonctionnalités de diagnostic pour les informations de journalisation provenant du serveur Web et de l'application web.</p><p>Ces informations sont réparties, en toute logique, en diagnostics de serveur web et en diagnostics d’application</p>|

## <a id="identify-sensitive-entities"></a>Vérifier que l’audit des connexions est activé sur SQL Server

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Base de données | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Configurer l’audit de connexion](https://msdn.microsoft.com/library/ms175850.aspx) |
| **Étapes** | <p>L’audit de connexion du serveur de bases de données doit être activé pour détecter/confirmer les attaques visant à deviner les mots de passe. Il est important de capturer les échecs de tentatives de connexion. La capture des échecs et réussites de tentatives de connexion offre des avantages supplémentaires pendant les investigations</p>|

## <a id="threat-detection"></a>Activer la détection des menaces sur SQL Azure

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Base de données | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | SQL Azure |
| **Attributs**              | Version SQL - V12 |
| **Informations de référence**              | [Prise en main de Threat Detection pour la base de données SQL](https://azure.microsoft.com/documentation/articles/sql-database-threat-detection-get-started/)|
| **Étapes** |<p>Threat Detection permet de détecter les activités base de données anormales indiquant la présence potentielle de menaces de sécurité pour la base de données. Elle fournit une nouvelle couche de sécurité qui permet aux clients de détecter les menaces potentielles et d’y répondre à mesure qu’elles se présentent en générant des alertes de sécurité sur les activités anormales.</p><p>Les utilisateurs peuvent explorer les événements suspects à l’aide de l’audit de base de données SQL Azure pour déterminer s’ils sont le résultat d’une tentative d’accès, d’une violation ou d’une exploitation des données dans la base de données.</p><p>Threat Detection vous permet de réagir facilement aux menaces potentielles à la base de données sans avoir à acquérir une expertise de la sécurité ou à gérer des systèmes de surveillance de la sécurité avancés</p>|

## <a id="analytics"></a>Utiliser Azure Storage Analytics pour auditer l’accès d’Azure Storage

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Azure Storage | 
| **Phase SDL**               | Déploiement |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A |
| **Informations de référence**              | [Utilisation de Storage Analytics pour surveiller le type d’autorisation](https://azure.microsoft.com/documentation/articles/storage-security-guide/#storage-analytics) |
| **Étapes** | <p>Pour chaque compte de stockage, l’utilisateur peut activer Azure Storage Analytics pour effectuer la journalisation et stocker les données de métriques. Les journaux d’analyse du stockage fournissent des informations importantes comme la méthode d’authentification utilisée par un utilisateur lors de l’accès au stockage.</p><p>Cela peut être très utile si vous surveillez étroitement l’accès au stockage. Par exemple, dans Blob Storage, vous pouvez définir tous les conteneurs comme privés et implémenter l’utilisation d’un service SAP dans toutes vos applications. Vous pouvez alors vérifier régulièrement les journaux pour voir si vos objets blob font l’objet d’un accès à l’aide de clés de compte de stockage, ce qui peut indiquer une violation de la sécurité, ou si les objets blob sont publics alors qu’ils ne devraient pas l’être.</p>|

## <a id="sufficient-logging"></a>Implémenter une journalisation suffisante

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | WCF | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | .NET Framework |
| **Attributs**              | N/A  |
| **Informations de référence**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Étapes** | <p>L’absence d’une piste d’audit correcte après un incident de sécurité peut entraver les efforts d’investigation. Windows Communication Foundation (WCF) offre la possibilité d’enregistrer les tentatives d’authentification ayant réussi et/ou échoué.</p><p>La journalisation des tentatives d’authentification ayant échoué peut avertir les administrateurs de potentielles attaques en force brute. De même, la journalisation des événements d’authentification ayant réussi peut fournir à une piste d’audit utile lorsqu’un compte légitime est compromis. Activer la fonctionnalité d’audit de la sécurité de service de WCF |

### <a name="example"></a>Exemple
Voici un exemple de configuration dans lequel l’audit est activé
```
<system.serviceModel>
    <behaviors>
        <serviceBehaviors>
            <behavior name=""NewBehavior"">
                <serviceSecurityAudit auditLogLocation=""Default""
                suppressAuditFailure=""false"" 
                serviceAuthorizationAuditLevel=""SuccessAndFailure""
                messageAuthenticationAuditLevel=""SuccessAndFailure"" />
                ...
            </behavior>
        </servicebehaviors>
    </behaviors>
</system.serviceModel>
```

## <a id="audit-failure-handling"></a>Implémenter une gestion suffisante des échecs d’audit

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | WCF | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | .NET Framework |
| **Attributs**              | N/A  |
| **Informations de référence**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Étapes** | <p>La solution développée est configurée pour ne pas générer d’exception lorsqu’elle ne parvient pas à écrire dans un journal d’audit. Si WCF est configuré pour ne pas lever une exception lorsqu’il ne parvient pas à écrire dans un journal d’audit, le programme n’est pas informé de l’échec et l’audit des événements de sécurité critiques ne peut pas être réalisé.</p>|

### <a name="example"></a>Exemple
L’élément `<behavior/>` du fichier de configuration WCF ci-dessous indique à WCF de ne pas informer l’application lorsqu’il ne parvient pas à écrire dans un journal d’audit.
````
<behaviors>
    <serviceBehaviors>
        <behavior name="NewBehavior">
            <serviceSecurityAudit auditLogLocation="Application"
            suppressAuditFailure="true"
            serviceAuthorizationAuditLevel="Success"
            messageAuthenticationAuditLevel="Success" />
        </behavior>
    </serviceBehaviors>
</behaviors>
````
Configurez WCF pour informer le programme chaque fois qu’il ne parvient pas à écrire dans un journal d’audit. Un autre schéma de notification doit être en place dans le programme pour alerter l’organisation que les pistes d’audit ne sont pas conservées. 

## <a id="logging-web-api"></a>Vérifier que l’audit et la journalisation sont appliqués à l’API web

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | API Web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | Activez l’audit et la journalisation sur les API web. Les journaux d’audit doivent capturer le contexte de l’utilisateur. Identifiez tous les événements importants et enregistrez ces événements. Implémenter la journalisation centralisée |

## <a id="logging-field-gateway"></a>Vérifier que l’audit et la journalisation appropriés sont appliqués sur la passerelle de champ

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Passerelle de champ IoT | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | <p>Lorsque plusieurs appareils se connectent à une passerelle de champ, vérifiez que les tentatives de connexion et l’état d’authentification (réussite ou échec) des appareils individuels sont enregistrés et conservés sur la passerelle de champ.</p><p>De plus, lorsque la passerelle de champ conserve les informations d’identification IoT Hub d’appareils individuels, vérifiez que l’audit est effectué lorsque ces informations d’identification sont récupérées. Développez un processus pour télécharger régulièrement les journaux dans Azure IoT Hub/Storage pour une rétention sur le long terme.</p> |

## <a id="logging-cloud-gateway"></a>Vérifier que l’audit et la journalisation appropriés sont appliqués sur la passerelle de cloud

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Passerelle de cloud IoT | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Introduction à la surveillance des opérations IoT Hub](https://azure.microsoft.com/documentation/articles/iot-hub-operations-monitoring/) |
| **Étapes** | <p>Concevez la collecte et le stockage des données d’audit collectées via la surveillance des opérations IoT Hub. Activez les catégories de surveillance suivantes :</p><ul><li>Opérations d’identité des appareils</li><li>Communications appareil-à-cloud</li><li>Communications cloud-à-appareil</li><li>connexions</li><li>Chargements de fichiers</li></ul>|