---
title: "aaaAuditing et journalisation - outil de modélisation des menaces Microsoft - Azure | Documents Microsoft"
description: "mesures d’atténuation des menaces exposé Bonjour outil de modélisation des menaces"
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
ms.openlocfilehash: f28988833eba251b6ceb8bbd47cde37e871af609
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-auditing-and-logging--mitigations"></a>Infrastructure de sécurité : Audit et journalisation | Corrections 
| Produit/service | Article |
| --------------- | ------- |
| **Dynamics CRM**    | <ul><li>[Identifier les entités sensibles dans votre solution et implémenter l’audit des modifications](#sensitive-entities)</li></ul> |
| **Application web** | <ul><li>[Vérifiez que l’audit et la journalisation est appliquée sur l’application hello](#auditing)</li><li>[Vérifier que la rotation et la séparation des journaux sont en place](#log-rotation)</li><li>[Vérifiez qu’application hello n’enregistre pas les données utilisateur sensibles](#log-sensitive-data)</li><li>[Vérifier que l’accès aux fichiers d’audit et journaux est restreint](#log-restricted-access)</li><li>[Vérifier que les événements de gestion des utilisateurs sont enregistrés](#user-management)</li><li>[Vérifiez que hello système intégrés défenses contre une mauvaise utilisation](#inbuilt-defenses)</li><li>[Activer la journalisation des diagnostics pour les applications web dans Azure App Service](#diagnostics-logging)</li></ul> |
| **Base de données** | <ul><li>[Vérifier que l’audit des connexions est activé sur SQL Server](#identify-sensitive-entities)</li><li>[Activer la détection des menaces sur SQL Azure](#threat-detection)</li></ul> |
| **Azure Storage** | <ul><li>[Utilisez l’accès tooaudit Analytique de stockage Azure du stockage Azure](#analytics)</li></ul> |
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

## <a id="auditing"></a>Vérifiez que l’audit et la journalisation est appliquée sur l’application hello

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
| **Étapes**                   | <p>La rotation des journaux est un processus automatisé utilisé dans l’administration système dans lequel les fichiers journaux obsolètes sont archivés. Les serveurs qui exécutent des applications de grande taille souvent journaliser chaque demande : en face de hello de journaux volumineux, rotation des journaux est un Bonjour toolimit de façon taille totale des journaux de hello tout en autorisant toujours une analyse des événements récents. </p><p>Séparation du journal signifie que vous avez toostore vos fichiers journaux sur une autre partition que votre système d’exploitation/application exécutant dans l’ordre tooavert un déni de service attaquent ou hello rétrogradation de votre application, ses performances</p>|

## <a id="log-sensitive-data"></a>Vérifiez qu’application hello n’enregistre pas les données utilisateur sensibles

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes**                   | <p>Vérifiez que ne pas ouvrir de session toutes les données sensibles qu’un utilisateur soumet tooyour site. Vérifiez la journalisation intentionnelle, ainsi que les effets secondaires dus à des problèmes de conception. Voici quelques exemples de données sensibles :</p><ul><li>Informations d’identification de l’utilisateur</li><li>Numéro de sécurité sociale ou autres informations d’identification</li><li>Numéros de carte de crédit ou autres informations financières</li><li>Informations de santé</li><li>Les clés privées ou autres données qui peut être utilisé toodecrypt des informations cryptées</li><li>Informations système ou une application qui peuvent être utilisées toomore attaques efficacement application hello</li></ul>|

## <a id="log-restricted-access"></a>Vérifier que l’accès aux fichiers d’audit et journaux est restreint

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes**                   | <p>Vérifiez tooensure accéder aux droits toolog fichiers sont correctement définies. Les comptes d’application doivent disposer d’un accès en écriture seule, et les opérateurs et le personnel de support doit disposer d’un accès en lecture seule en fonction des besoins.</p><p>Les comptes administrateurs sont hello seuls comptes qui doivent avoir un accès complet. Vérifier le QU'ACL de Windows sur le journal des fichiers tooensure qu’ils sont correctement limités :</p><ul><li>Les comptes d’application doivent disposer d’accès en écriture seule</li><li>Les opérateurs et le personnel de support doivent disposer d’un accès en lecture seule en fonction des besoins</li><li>Les administrateurs sont hello seuls les comptes doivent avoir un accès complet</li></ul>|

## <a id="user-management"></a>Vérifier que les événements de gestion des utilisateurs sont enregistrés

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes**                   | <p>Assurez-vous qu’application hello surveille les événements de gestion d’utilisateur tels que les connexions de l’utilisateur ayant réussi et ayant échoué, réinitialisation de mot de passe, les modifications de mot de passe, le verrouillage de compte, enregistrement de l’utilisateur. Cette opération permet de toodetect et réagit toopotentially un comportement suspect. Il permet également de données d’opérations toogather ; par exemple, tootrack qui est à l’application hello</p>|

## <a id="inbuilt-defenses"></a>Vérifiez que hello système intégrés défenses contre une mauvaise utilisation

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes**                   | <p>Les contrôles permettant de lever des exceptions de sécurité en cas de mauvaise utilisation de l’application doivent être en place. Par exemple, si la validation d’entrée est en place et un attaquant tente tooinject un code malveillant qui ne correspond pas hello regex, une exception de sécurité peut levée qui peut être un simple d’une mauvaise utilisation du système</p><p>Par exemple, il est recommandé d’exceptions de sécurité toohave connectées et les actions effectuées pour hello suivants :</p><ul><li>Validation des entrées</li><li>Violations CSRF</li><li>Force brute (limite supérieure du nombre de requêtes par utilisateur et par ressource)</li><li>Violations de chargement de fichiers</li><ul>|

## <a id="diagnostics-logging"></a>Activer la journalisation des diagnostics pour les applications web dans Azure App Service

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | EnvironmentType - Azure |
| **Informations de référence**              | N/A  |
| **Étapes** | <p>Azure fournit tooassist diagnostics intégrés avec le débogage d’un Service d’application web app. Il s’applique également tooAPI applications et des applications mobiles. Applications de Service d’applications web fournissent des fonctionnalités de diagnostic enregistrées les informations de serveur web de hello et application web de hello.</p><p>Ces informations sont réparties, en toute logique, en diagnostics de serveur web et en diagnostics d’application</p>|

## <a id="identify-sensitive-entities"></a>Vérifier que l’audit des connexions est activé sur SQL Server

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Base de données | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Configurer l’audit de connexion](https://msdn.microsoft.com/library/ms175850.aspx) |
| **Étapes** | <p>L’audit des connexions serveur de base de données doit être activé toodetect/confirmer un mot de passe estimation des attaques. Il est important de tentatives de connexion qui ont échoué toocapture. La capture des échecs et réussites de tentatives de connexion offre des avantages supplémentaires pendant les investigations</p>|

## <a id="threat-detection"></a>Activer la détection des menaces sur SQL Azure

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Base de données | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | SQL Azure |
| **Attributs**              | Version SQL - V12 |
| **Informations de référence**              | [Prise en main de Threat Detection pour la base de données SQL](https://azure.microsoft.com/documentation/articles/sql-database-threat-detection-get-started/)|
| **Étapes** |<p>La détection des menaces détecte des activités de base de données anormales indiquant de base de données des toohello des menaces de sécurité potentielles. Il fournit une nouvelle couche de sécurité, ce qui permet aux clients toodetect et de répond toopotential menaces qu’ils se produisent en fournissant des alertes de sécurité sur les activités anormales.</p><p>Les utilisateurs peuvent Explorer à l’aide d’Azure SQL Database Auditing toodetermine s’ils résultent d’une tentative de tooaccess, violation d’événements suspects hello ou exploiter les données dans la base de données hello.</p><p>La détection des menaces rend tooaddress simple potentiels menaces toohello base de données sans nécessité de hello toobe un expert en sécurité ou gérer des systèmes de surveillance de la sécurité avancée</p>|

## <a id="analytics"></a>Utilisez l’accès tooaudit Analytique de stockage Azure du stockage Azure

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Azure Storage | 
| **Phase SDL**               | Déploiement |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A |
| **Informations de référence**              | [À l’aide du type de stockage Analytique toomonitor d’autorisation](https://azure.microsoft.com/documentation/articles/storage-security-guide/#storage-analytics) |
| **Étapes** | <p>Pour chaque compte de stockage, un qui peut activer la journalisation de tooperform Analytique de stockage Azure et stocker les données de métriques. journaux d’analytique Hello stockage fournissent des informations importantes telles que de la méthode d’authentification utilisée par un utilisateur lors de l’accès au stockage.</p><p>Cela peut être très utile si vous sont protégeant étroitement les accès toostorage. Par exemple, dans le stockage Blob, vous pouvez définir toutes tooprivate de conteneurs hello et implémenter utilisez hello d’un service SAS dans l’ensemble de vos applications. Vous pouvez vérifier hello enregistre régulièrement toosee si vos objets BLOB est accessibles à l’aide de clés de compte de stockage hello, ce qui peuvent indiquer une violation de la sécurité, ou si les objets BLOB de hello sont publics, mais ils ne doivent pas être.</p>|

## <a id="sufficient-logging"></a>Implémenter une journalisation suffisante

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | WCF | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | .NET Framework |
| **Attributs**              | N/A  |
| **Informations de référence**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Étapes** | <p>absence de Hello d’une piste d’audit corrects après un incident de sécurité peut entraver les efforts d’investigation. Windows Communication Foundation (WCF) propose des tentatives d’authentification ayant réussi ou échoué hello capacité toolog.</p><p>La journalisation des tentatives d’authentification ayant échoué peut avertir les administrateurs de potentielles attaques en force brute. De même, la journalisation des événements d’authentification ayant réussi peut fournir à une piste d’audit utile lorsqu’un compte légitime est compromis. Activer la fonctionnalité d’audit de la sécurité de service de WCF |

### <a name="example"></a>Exemple
Hello Voici un exemple de configuration avec l’audit activé
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
| **Étapes** | <p>Solution développée est configurée pas toogenerate une exception en cas d’échec de journal d’audit de tooan toowrite. Si WCF est configuré pas toothrow une exception lorsqu’il est le journal d’audit de tooan toowrite impossible, programme de hello n’est pas informé de défaillance de hello et l’audit des événements de sécurité critique peut ne pas survenir.</p>|

### <a name="example"></a>Exemple
Hello `<behavior/>` élément du fichier de configuration WCF hello ci-dessous indique à WCF toonot notifier l’application hello lorsque WCF ne parvient pas le journal d’audit de tooan toowrite.
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
Configurer le programme WCF toonotify hello chaque fois qu’il est le journal d’audit de tooan toowrite impossible. programme de Hello doit avoir un schéma de notification secondaire dans l’organisation de hello tooalert lieu que les pistes d’audit ne sont pas conservées. 

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
| **Étapes** | <p>Lorsque plusieurs appareils connectent tooa passerelle de champ, assurez-vous que les tentatives de connexion et l’état d’authentification (réussite ou échec) pour les appareils individuels sont enregistrées et conservées sur hello passerelle de champ.</p><p>En outre, dans les cas où le champ passerelle est en conservant hello IoT Hub les informations d’identification pour des périphériques, assurez-vous que l’audit est effectuée lorsque ces informations d’identification sont récupérées. Développer un processus tooperiodically téléchargement hello journaux tooAzure IoT Hub/du stockage pour une rétention à long terme.</p> |

## <a id="logging-cloud-gateway"></a>Vérifier que l’audit et la journalisation appropriés sont appliqués sur la passerelle de cloud

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Passerelle de cloud IoT | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Surveillance des opérations introduction tooIoT Hub](https://azure.microsoft.com/documentation/articles/iot-hub-operations-monitoring/) |
| **Étapes** | <p>Concevez la collecte et le stockage des données d’audit collectées via la surveillance des opérations IoT Hub. Activer hello suivant analyses catégories :</p><ul><li>Opérations d’identité des appareils</li><li>Communications appareil-à-cloud</li><li>Communications cloud-à-appareil</li><li>connexions</li><li>Chargements de fichiers</li></ul>|
