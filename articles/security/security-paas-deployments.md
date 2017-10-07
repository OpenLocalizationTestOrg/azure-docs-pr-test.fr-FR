---
title: "les déploiements PaaS aaaSecuring | Documents Microsoft"
description: " Découvrir les avantages de sécurité hello de PaaS et autres modèles de service cloud et des pratiques recommandées pour la sécurisation de votre déploiement PaaS Azure. "
services: security
documentationcenter: na
author: techlake
manager: MBaldwin
editor: techlake
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2017
ms.author: terrylan
ms.openlocfilehash: b94fe03b6f3a43d82e1e6e834f10a423e4c1db95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-paas-deployments"></a>Sécurisation des déploiements PaaS

Cet article fournit des informations qui vous permettent :

- Comprendre les avantages de sécurité hello d’hébergement d’applications dans le cloud de hello
- Évaluer les avantages de sécurité hello de plateforme en tant que service (PaaS) et autres modèles de service cloud
- Modifier le focus de la sécurité d’une approche de sécurité de périmètre centré sur l’identité tooan centrée sur le réseau
- d'implémenter les bonnes pratiques recommandées de la sécurité de la PaaS.

## <a name="cloud-security-advantages"></a>Avantages du cloud en matière de sécurité
Il existe toobeing des avantages de sécurité dans le cloud de hello. Dans un environnement sur site, les organisations disposent probablement non remplies responsabilités et des ressources limitées de tooinvest disponible dans la sécurité, ce qui crée un environnement où les attaquants tooexploit en mesure des vulnérabilités à tous les niveaux.

![Les avantages de l’ère du cloud en matière de sécurité][1]

Les organisations est en mesure de tooimprove leur détection des menaces et les temps de réponse à l’aide des fonctionnalités de sécurité basée sur le cloud et l’intelligence de cloud d’un fournisseur.  En utilisant le fournisseur de cloud de responsabilités toohello, organisations peuvent obtenir plus garantie de sécurité, ce qui leur permet tooreallocate les ressources de sécurité et les priorités de l’entreprise tooother budget.

## <a name="division-of-responsibility"></a>Répartition de la responsabilité
Il s’agit de division de hello toounderstand important de responsabilité entre vous et Microsoft. En local, vous possédez l’ensemble de la pile hello mais que vous vous déplacez toohello cloud certaines responsabilités de transfert tooMicrosoft. Hello responsabilité tableau ci-dessous indique les zones hello de pile de hello dans un déploiement IaaS, PaaS et SaaS dont vous êtes responsable et Microsoft est responsable.

![Zones de responsabilité][2]

Vous avez vos données et les identités pour tous les types de déploiement dans le cloud. Vous êtes responsable de la protection de sécurité hello de vos données et les identités, des ressources locales et hello composants cloud que vous contrôlez (qui varie selon le type de service).

Les responsabilités sont toujours conservées par vous, quel que soit le type de hello de déploiement, sont :

- Données
- Endpoints
- Compte
- gestion de l’accès

## <a name="security-advantages-of-a-paas-cloud-service-model"></a>Avantages d'un modèle de service cloud PaaS en matière de sécurité
À l’aide de hello même matrice de responsabilité, nous allons examiner les avantages de sécurité hello d’un déploiement PaaS Azure et locaux.

![Les avantages d'une PaaS en matière de sécurité][3]

Bas hello pile hello, infrastructure physique hello Microsoft atténue responsabilités et les risques courants. Hello cloud de Microsoft est surveillée en permanence par Microsoft, il est difficile tooattack. Il n’a aucune signification pour un hello de toopursue attaquant cloud de Microsoft en tant que cible. À moins que les intrus hello possède un grand nombre d’argent et de ressources, les intrus hello est probablement toomove sur tooanother cible.  

Milieu hello de pile de hello, il n’existe aucune différence entre un déploiement PaaS et sur site. Couche d’application hello et la couche de gestion de compte et un accès hello, vous disposez des risques similaires. Dans la section hello suivante étapes de cet article, nous vous guide pratiques toobest pour éliminer ou réduire ces risques.

Haut hello de pile de hello, gouvernance des données et la gestion des droits, vous prenez un risque qui peut être atténué par la gestion de clés. (la gestion des clés est traitée dans les bonnes pratiques). Lors de la gestion de clés est une responsabilité supplémentaire, vous avez des zones dans un déploiement PaaS que vous n’avez plus toomanage donc vous pouvez décaler la gestion des ressources tookey.

Hello plateforme Azure fournit également une protection DDoS renforcée à l’aide de différentes technologies de réseau. Toutefois, tous les types de méthodes de protection contre le déni de service distribué (DDoS) basée sur le réseau ont leurs limites par lien et par centre de données. toohelp éviter impact hello de grandes attaques DDoS, vous pouvez tirer parti de la fonctionnalité cloud d’Azure core destinée à vous tooquickly et automatiquement montée en puissance parallèle toodefend contre des attaques DDoS. Nous aborderons plus en détail sur comment vous pouvez faire cela dans hello recommandé pratiques articles.

## <a name="modernizing-hello-defenders-mindset"></a>État d’esprit du modernisation defender hello
Les déploiements PaaS accompagnent une équipe dans votre toosecurity approche globale. Vous déplacez d’avoir toocontrol tout vous-même responsabilité toosharing avec Microsoft.

Une autre différence importante entre PaaS et des déploiements sur site traditionnelle, est une nouvelle vue de ce que définit le périmètre de sécurité principal hello. Historiquement, périmètre de sécurité locale principale hello était votre réseau et plus local sécurité conceptions utilisez hello réseau comme son pivot principal de sécurité. Pour les déploiements PaaS, il est préférable en tenant compte du périmètre de sécurité principal identité toobe hello.

## <a name="identity-as-hello-primary-security-perimeter"></a>Identité que le périmètre de sécurité principal hello
Une des cinq caractéristiques essentielles hello du cloud computing est un large accès réseau, ce qui rend centrée sur le réseau considérant moins pertinentes. objectif Hello d’une grande partie du cloud computing est tooallow utilisateurs tooaccess des ressources, quelle que soit l’emplacement. Pour la plupart des utilisateurs, leur emplacement va toobe quelque part sur hello Internet.

Hello figure suivante montre comment le périmètre de sécurité hello a évolué à partir d’un réseau de périmètre d’identité périmètre tooan. La sécurité devient plus ou moins sur la protection de votre réseau sur la protection de vos données, ainsi que gestion de la sécurité hello de vos applications et les utilisateurs. Hello principale différence est que vous souhaitez société d’importantes tooyour de toopush sécurité proche toowhat.

![L'identité en tant que nouveau périmètre de sécurité][4]

Initialement, les services PaaS Azure (par exemple, les rôles web et Azure SQL) fournissaient peu ou pas de défenses du périmètre de réseau traditionnelles. Il a été entendu qu’objectif de l’élément hello est toobe exposée toohello Internet (rôle web) et que l’authentification hello nouveau périmètre (par exemple, un objet BLOB ou SQL Azure).

Pratiques de sécurité modernes partent du principe qu’adversaire hello a enfreint le périmètre du réseau hello. Par conséquent, les pratiques de défense modernes ont déplacés tooidentity. Les organisations doivent établir un périmètre de sécurité basé sur les identités avec forte hygiène d’authentification et d’autorisation (bonnes pratiques).

## <a name="recommendations-for-managing-hello-identity-perimeter"></a>Recommandations pour la gestion du périmètre d’identité hello

Principes et des modèles pour le réseau de périmètre hello ont été disponibles des dizaines d’années. En revanche, secteur d’activité hello possède relativement moins expérience à l’aide d’identité en tant que le périmètre de sécurité principal hello. Cela étant dit, nous ont accumulé suffisamment tooprovide expérience quelques recommandations générales qui sont prouvées dans le champ de hello et appliquer tooalmost tous les services PaaS.

Hello Voici une toomanaging d’approche meilleures pratiques générales du périmètre de votre identité.

- **Ne perdez pas vos clés ou les informations d’identification** sécurisation des clés et les informations d’identification est essentielle toosecure les déploiements PaaS. La perte de clés ou d'informations d’identification est un problème courant. Toouse une solution centralisée est une bonne solution dans laquelle les clés et les secrets peuvent être stockées dans des modules de sécurité matériel (HSM). Azure fournit un module HSM dans le cloud hello avec [Azure Key Vault](../key-vault/key-vault-whatis.md).
- **Ne placez les informations d’identification et d’autres secrets dans le code source ou GitHub** hello uniquement pire que perdre vos clés et les informations d’identification rencontre une partie non autorisée obtenir accès toothem. Les personnes malveillantes sont parti tootake en mesure de clés de toofind bot technologies et des clés secrètes stockées dans des référentiels de code, tels que GitHub. Ne placez pas de clé et de secrets dans ces référentiels de code source publics.
- **Protégez vos interfaces de gestion de machine virtuelle sur des services PaaS et IaaS hybrides** Les services IaaS et PaaS s’exécutent sur des machines virtuelles (VM). En fonction de type hello de service, plusieurs interfaces de gestion sont disponibles qui permettent de tooremote gérer ces ordinateurs virtuels directement. Vous pouvez utiliser les protocoles de gestion à distance tels que [le protocole SSH (Secure Shell)](https://en.wikipedia.org/wiki/Secure_Shell), [le protocole RDP (Remote Desktop)](https://support.microsoft.com/kb/186607) et [PowerShell distant](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/enable-psremoting). En règle générale, nous vous recommandons de ne pas activer tooVMs d’accès à distance directe à partir de hello Internet. S’il est disponible, vous devez utiliser d'autres approches, telles que l’utilisation d’un réseau privé virtuel dans un réseau virtuel Azure. Si aucune autre approche n'est disponible, assurez-vous que vous utilisez des phrases secrètes complexes et, si d'autres options sont disponibles, l’authentification à deux facteurs (notamment [Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)).
- **Utilisez une authentification forte et des plateformes d’autorisation**

  - Utilisez des identités fédérées dans Azure AD au lieu des magasins d’utilisateurs personnalisés. Lorsque vous utilisez des identités fédérées, vous tirer parti d’une approche basée sur la plateforme et vous déléguer la gestion de hello de partenaires de tooyour identités autorisés. Une approche d’identité fédérée est particulièrement importante dans les scénarios lorsque les employés sont terminées et que les informations doivent toobe réfléchie par l’intermédiaire de plusieurs identités et d’autorisation systèmes.
  - Utilisez des mécanismes d'authentification et d'autorisation basés sur des plateformes au lieu d'un code personnalisé. Hello parce que le développement de code d’authentification personnalisé peut être sujette aux erreurs. La plupart de vos développeurs n’est pas des experts en sécurité et est peu probable toobe connaître les subtilités hello et hello derniers développements de l’authentification et l’autorisation. Le code commercial (par exemple par Microsoft) est souvent contrôlé en ce qui concerne la sécurité.
  - Utilisez l'authentification multifacteur. L’authentification multifacteur est en cours de hello standard pour l’authentification et l’autorisation car elle évite les failles de sécurité hello inhérents aux types de nom d’utilisateur et mot de passe d’authentification. Interfaces d’accès aux tooboth hello Azure management (portal remote PowerShell) et toocustomer services exposés au doit être conçus et configuré toouse [Azure multi-Factor Authentication (MFA)](../multi-factor-authentication/multi-factor-authentication.md).
  - Utilisez des protocoles d’authentification standard, tels qu'OAuth2 et Kerberos. Ces protocoles ont été largement contrôlés et sont probablement implémentés dans le cadre de vos bibliothèques de plateforme pour l’authentification et l’autorisation.

## <a name="next-steps"></a>Étapes suivantes
Dans cet article, nous avons vu les avantages d’un déploiement PaaS Azure en matière de sécurité. Découvrez ensuite les pratiques recommandées pour sécuriser solutions PaaS web et mobiles. Nous allons commencer par Azure App Service, Azure SQL Database et Azure SQL Data Warehouse. Lorsque des articles sur les pratiques recommandées pour les autres services Azure sont disponibles, des liens seront fournies dans hello suivant liste :

- [Azure App Service](security-paas-applications-using-app-services.md)
- [Azure SQL Database et Azure SQL Data Warehouse](security-paas-applications-using-sql.md)
- Azure Storage
- Cache REDIS Azure
- Azure Service Bus
- Pare-feu d’applications web

<!--Image references-->
[1]: ./media/security-paas-deployments/advantages-of-cloud.png
[2]: ./media/security-paas-deployments/responsibility-zones.png
[3]: ./media/security-paas-deployments/advantages-of-paas.png
[4]: ./media/security-paas-deployments/identity-perimeter.png
