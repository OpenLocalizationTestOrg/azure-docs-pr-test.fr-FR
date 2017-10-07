---
title: "fonctionnalités de sécurité du réseau aaaProtect des données personnelles avec Azure | Documents Microsoft"
description: "Protéger les données personnelles à l’aide des fonctionnalités de sécurité réseau Azure"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: be112a9408d327ccedf871656afe800fc7f775e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="protect-personal-data-with-network-security-features-azure-application-gateway-and-network-security-groups"></a>Protéger les données personnelles avec les fonctionnalités de sécurité réseau : Azure Application Gateway et groupes de sécurité réseau

Cet article fournit des informations et des procédures qui vous aideront à utiliser la passerelle d’Application Azure et les groupes de sécurité réseau tooprotect les données personnelles.

Un élément important à une sécurité multicouche stratégie tooprotect hello assurer la confidentialité des données personnelles est une protection contre les attaques de vulnérabilité courantes telles que l’injection SQL ou de scripts entre sites. Conserver le trafic indésirable de votre réseau virtuel Azure vous protège contre avéré des données sensibles et permet de Microsoft Azure toohelp d’outils vous protéger vos données contre les pirates.

## <a name="scenario"></a>Scénario

Une société de croisière volumineux en hello États-Unis, étend ses itinéraires de toooffer d’opérations dans hello Méditerranée, Adriatique et mer Baltique, ainsi que hello britanniques. Dans le cadre de ces efforts, elle a acquis plusieurs plus petits croisière Royaume-Uni Italie, Allemagne, Danemark et hello basée sur des lignes

la société de Hello utilise Microsoft Azure toostore des données d’entreprise Bonjour de cloud computing et exécuter des applications sur des machines virtuelles qui traitent et accéder à ces données. Ces dernières incluent des informations d’identification personnelle telles que les noms, les adresses, les numéros de téléphone et les informations de carte de crédit de sa base de clients globale. Il inclut également des informations de ressources humaines traditionnelles telles que les adresses et numéros de téléphone, numéros d’identification de taxe médicales plus d’informations sur les employés de la société dans tous les emplacements. ligne de croisière Hello gère également les bases de données volumineuses de membres du programme de récompense et fidélité qui inclut des informations personnelles tootrack des relations avec les clients en cours et passées.

Réseau de hello accès employés de l’entreprise à partir de sites distants et les agents de voyage dans Bonjour société hello ont accès aux ressources de l’entreprise toosome et utiliser des applications web hébergées dans toointeract de machines virtuelles Azure avec lui.

## <a name="problem-statement"></a>Définition du problème

société de Hello doit protéger la confidentialité de hello de clients et les données personnelles employés les attaquants qui exploitent les vulnérabilités toorun malveillant code logiciel qui peut exposer des données personnelles stockées ou utilisée par les applications en cloud hello entreprise.

## <a name="company-goal"></a>Objectif de l’entreprise

Hello tooensure objectif de l’entreprise non autorisée de personnes ne peut pas accéder à des réseaux virtuels Azure d’entreprise et les applications hello et les données qui y résident en exploitant les vulnérabilités courantes. 

## <a name="solutions"></a>Solutions

Microsoft Azure offre une sécurité mécanismes toohelp empêcher le trafic indésirable d’entrer des réseaux virtuels Azure. Le contrôle du trafic entrant et sortant est généralement effectué par des pare-feu. Dans Azure, vous pouvez utiliser hello passerelle d’Application avec hello pare-feu d’applications Web et les groupes de sécurité de réseau (NSG), qui agissent en tant qu’un pare-feu distribué simple. Ces outils vous toodetect et bloquent le trafic réseau indésirables.

### <a name="application-gatewayweb-application-firewall"></a>Application Gateway/Pare-feu d’applications web

Hello [pare-feu d’applications Web](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview) composant (WAF) de hello [passerelle d’Application Azure](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) protège les applications web qui sont plus en plus des cibles des attaques malveillantes connues commun d’exploiter vulnérabilités. Un WAF centralisé permet de se prémunir à la fois contre les attaques web et de simplifier la gestion de la sécurité sans avoir à modifier l’application.

Le WAF Azure traite différentes catégories d’attaques, notamment l’injection de code SQL, les scripts de site à site, les violations et anomalies de protocole HTTP, les robots, les scanneurs, les erreurs de configuration d’application courantes, le déni de service HTTP et d’autres attaques courantes comme l’injection de commandes, la dissimulation de requête HTTP, le fractionnement de réponse HTTP et les attaques par inclusion de fichier distant. 

Vous pouvez créer une passerelle d’application avec WAF ou ajouter la passerelle d’application WAF tooan existant. Dans les deux cas, Azure Application Gateway requiert son propre sous-réseau.

#### <a name="how-do-i-create-an-application-gateway-with-waf"></a>Comment créer une passerelle d’application avec WAF ? 

toocreate une nouvelle passerelle d’application avec WAF activé, hello suivant :

1. Journal dans toohello portail Azure et hello **favoris** volet hello du portail de, cliquez sur **nouveau**

2. Bonjour **nouveau** panneau, cliquez sur **réseau**.

3. Cliquez sur **Application Gateway**.

4. Accédez toohello portail Azure, **cliquez sur Nouveau \> réseau \> passerelle d’Application.**

   ![création de passerelles d’application](media/protect-netsec/app-gateway-01.png)

5. Bonjour **notions de base** panneau qui s’affiche, entrez les valeurs de hello pour hello suivant champs : nom, le niveau (Standard ou WAF), taille de référence (SKU) (petite, moyenne ou grande), (2 pour la haute disponibilité), de nombre d’instances abonnement, le groupe de ressources, et Emplacement.

6. Bonjour **paramètres** panneau s’affiche sous **réseau virtuel**, cliquez sur **choisir un réseau virtuel**. Cette étape s’ouvre entrez hello Panneau de réseau virtuel choisir.

7. Cliquez sur **nouvel** tooopen hello **créer un réseau virtuel** panneau.

8. Entrez hello valeurs suivantes : nom, l’espace d’adressage, nom du sous-réseau, plage d’adresses de sous-réseau. Cliquez sur **OK**.

9. Sur hello **paramètres** panneau sous **configuration Frontend IP**, choisissez le type d’adresse IP hello.

10. Cliquez sur **choisir une adresse IP publique,** puis **Créer un nouveau.**

11. Acceptez la valeur par défaut de hello, puis cliquez sur **OK.**

12. Sur hello **paramètres** panneau sous **configuration de l’écouteur**, sélectionnez toouse HTTP ou HTTPS sous **protocole**. toouse HTTPS, un certificat est requis.

13. Configurer les paramètres spécifiques de hello WAF : **état du pare-feu** (**activé**) et **mode pare-feu** (**prévention**). Si vous choisissez **détection** comme mode de hello, le trafic est enregistré uniquement.

14. Hello de révision **Résumé** page, puis cliquez sur **OK**. Maintenant la passerelle d’application hello est la file d’attente et créé.

Une fois la passerelle d’application hello a été créé, vous pouvez naviguer tooit dans le portail de hello et continuer la configuration de la passerelle d’application hello.

![passerelle d’application créée](media/protect-netsec/adatum-app-gateway.png)

#### <a name="how-do-i-add-waf-tooan-existing-application"></a>Comment ajouter des applications existantes de WAF tooan ?

tooupdate un WAF de toosupport passerelle application existante en mode de prévention, hello suivant :

1. Bonjour Azure portal **favoris** volet, cliquez sur **toutes les ressources**.

2. Cliquez sur hello passerelle d’Application existante dans hello **toutes les ressources** panneau. 
>[!NOTE]
Remarque : Si l’abonnement hello que déjà sélectionné comporte plusieurs ressources, vous pouvez entrer les nom hello Bonjour filtre par nom... zone DNS zone tooeasily accès hello.
3. Cliquez sur **pare-feu d’applications Web** et mettre à jour les paramètres de passerelle d’application hello : **mise à niveau tooWAF couche** (activée), **état du pare-feu** (activé),  **Mode de pare-feu** (prévention). Vous devez également tooconfigure hello ensemble de règles et configurer des règles désactivées.

Pour plus d’informations sur la façon de toocreate une nouvelle passerelle d’application avec WAF et comment tooadd WAF tooan application passerelle existante, consultez [créer une passerelle d’application avec le pare-feu d’applications web à l’aide du portail de hello.](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-portal)

### <a name="network-security-groups"></a>Network Security Group

A [groupe de sécurité réseau](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg) (NSG) contient une liste de règles de sécurité qui autorisent ou refusent tooresources de trafic réseau connecté trop[réseaux virtuels Azure](https://docs.microsoft.com/azure/virtual-network/) (VNet). Groupes de sécurité réseau peuvent être associé à toosubnets ou des ordinateurs virtuels individuels. Lorsqu’un groupe de sécurité réseau est associé tooa sous-réseau, les règles de hello s’appliquent tooall ressources toohello connecté sous-réseau. Le trafic peut encore être limité en également associer un tooa groupe de sécurité réseau de machine virtuelle ou la carte réseau.

Les NSG contiennent quatre propriétés : Nom, Région, Groupe de ressources et Règles.
>[!Note]
Bien qu’il existe un groupe de sécurité réseau dans un groupe de ressources, il peut être associé à tooresources dans n’importe quel groupe de ressources, tant que ressource de hello fait partie de hello même région Azure que hello groupe de sécurité réseau.

Les règles de NSG contiennent neuf propriétés : Nom, Protocole (TCP, UDP ou \*, qui inclut ICMP ainsi que UDP et TCP), Plage de ports source, Plage de ports de destination, Préfixe d’adresse source, Préfixe d’adresse de destination, Direction (entrant ou sortant), Priorité (comprise entre 100 et 4 096) et Type d’accès (autorisation ou refus). Tous les groupes de sécurité réseau contient un ensemble de règles par défaut qui peut être supprimé ou remplacé par des règles hello que vous créez.

#### <a name="how-do-i-implement-nsgs"></a>Comment implémenter des NSG ?

Implémentation de groupes de sécurité réseau nécessite une planification, et il existe plusieurs règles de conception vous devez tootake en compte. Ceux-ci incluent les limites de nombre de hello de groupes de sécurité réseau par abonnement et règles par groupe de sécurité réseau ; Conception de réseau virtuel et le sous-réseau, des règles spéciales, le trafic ICMP, isolation des niveaux de sous-réseaux, les équilibreurs de charge et bien plus encore.

Pour plus d’informations sur la planification et l’implémentation des NSG, ainsi que pour obtenir un exemple de scénario de déploiement, consultez [Filtrer le trafic réseau avec les groupes de sécurité réseau.](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg)

#### <a name="how-do-i-create-rules-in-an-nsg"></a>Comment créer des règles dans un NSG ?

toocreate règles dans un groupe de sécurité réseau existant de trafic entrant, hello suivant :

1. Cliquez sur **Parcourir**, puis sur **Groupes de sécurité réseau**.

2. Dans la liste de hello des groupes de sécurité réseau, cliquez sur **NSG-FrontEnd**, puis **les règles de sécurité de trafic entrant.**

3. Dans la liste de hello des règles de sécurité de trafic entrant, cliquez sur **ajouter.**

4. Entrez des valeurs de hello dans hello suivant champs : nom, la priorité, Source, protocole, Source de plage de Destination, Destination plage de ports et l’Action.

nouvelle règle de Hello apparaîtront dans hello NSG après quelques secondes.

![règles de sécurité réseau](media/protect-netsec/inbound-security.png)

Pour plus d’informations sur comment toocreate groupes de sécurité réseau dans des sous-réseaux, créer des règles et associer un groupe de sécurité réseau avec un sous-réseau frontal et principal, consultez [créer des groupes de sécurité réseau à l’aide de hello portail Azure.](https://docs.microsoft.com/azure/virtual-network/virtual-networks-create-nsg-arm-pportal)

## <a name="next-steps"></a>Étapes suivantes

[Sécurité du réseau Azure](https://azure.microsoft.com/blog/azure-network-security/)

[Bonnes pratiques en matière de sécurité du réseau Azure](https://docs.microsoft.com/azure/security/azure-security-network-security-best-practices)

[Obtenir des informations sur un groupe de sécurité réseau](https://docs.microsoft.com/rest/api/network/virtualnetwork/get-information-about-a-network-security-group)

[Pare-feu d’application web (WAF)](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview)
