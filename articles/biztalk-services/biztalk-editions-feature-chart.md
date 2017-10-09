---
title: "aaaLearn sur les fonctionnalités dans les éditions de BizTalk Services | Documents Microsoft"
description: "Comparer les fonctions hello des éditions de BizTalk Services hello : libérer, Developer, Basic, Standard et Premium. MABS, WABS."
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: c589629f-06b1-44bb-b8ca-1db71826ea59
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 81626fa743a7190e7c78a0fd90b3054a08982b02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-editions-chart"></a>Tableau comparatif des éditions de BizTalk Services

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Azure BizTalk Services offre plusieurs éditions. Utilisez cette toodetermine article quelle édition est adaptée aux besoins de votre scénario et des besoins.

## <a name="compare-hello-editions"></a>Comparer les éditions de hello
**Gratuite (Évaluation)**

Création et gestion des connexions hybrides. Une connexion hybride est un tooconnect facilement un site Web Azure de tooan système, telles que SQL Server sur site.

**Développeur**

Cette édition permet le traitement des messages des connexions hybrides, EAI et EDI grâce à un portail de gestion de partenaire commercial simple à utiliser, une prise en charge des schémas EDI répandus et des capacités de traitement EDI enrichies sur X12 et AS2. Créez les scénarios courants EAI connecter les services de cloud de hello avec n’importe quel tooread des protocoles HTTP/S, REST, FTP, WCF et SFTP et écrire des messages.  Utiliser des systèmes de connectivité local tooon métier à prêt à l’emploi des adaptateurs SAP, Oracle eBusiness, base de données Oracle, Siebel et SQL Server. Utilisez un environnement conçu pour les développeurs, doté d'outils Visual Studio, facilitant le développement et le déploiement. Limité toodevelopment et aux tests uniquement avec aucun contrat (SLA).

**De base**

Inclut la plupart des fonctionnalités pour les développeurs hello avec augmente dans les connexions de connexions hybrides, des ponts EAI, accords EDI et Pack d’adaptateurs BizTalk. Offre également une haute disponibilité et hello option tooscale avec un contrat de niveau de Service (SLA).

**Standard**

Inclut toutes les fonctionnalités de base hello avec augmente dans les connexions de connexions hybrides, des ponts EAI, accords EDI et Pack d’adaptateurs BizTalk. Offre également une haute disponibilité et hello option tooscale avec un contrat de niveau de Service (SLA).

**Premium**

Inclut toutes les fonctions Standard hello avec augmente dans les connexions de connexions hybrides, des ponts EAI, accords EDI et Pack d’adaptateurs BizTalk. Inclut également l’archivage, la haute disponibilité et hello option tooscale avec un contrat de niveau de Service (SLA).

## <a name="editions-chart"></a>Tableau comparatif des éditions
Hello tableau suivant répertorie les différences de hello.

<table border="1">
<tr bgcolor="FAF9F9">
        <th></th>
        <th>Gratuite (Évaluation)</th>
        <th>Développeur</th>
        <th>De base</th>
        <th>Standard</th>
        <th>Premium</th>
</tr>

<tr>
<td><strong>Prix de départ</strong></td>
<td colspan="5"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=304011"> Tarification Azure BizTalk Services</a> <br/><br/> <a HREF="http://azure.microsoft.com/pricing/calculator/?scenario=full"> Calculatrice de prix Azure</a></td>
</tr>
<tr>
<td><strong>Configuration minimale par défaut</strong></td>
<td>1 unité Gratuite</td>
<td>1 unité Développeur</td>
<td>1 unité De base</td>
<td>1 unité Standard</td>
<td>1 unité Premium</td>
</tr>
<tr>
<td><strong>Mettre à l'échelle</strong></td>
<td>Pas de mise à l'échelle</td>
<td>Pas de mise à l'échelle</td>
<td>Oui, dans les incréments d'1 unité De base</td>
<td>Oui, dans les incréments d'1 unité Standard</td>
<td>Oui, dans les incréments d'1 unité Premium</td>
</tr>
<tr>
<td><strong>Augmentation de la taille des instances maximum autorisée</strong></td>
<td>Pas de mise à l'échelle</td>
<td>Pas de mise à l'échelle</td>
<td>Unités de too8</td>
<td>Unités de too8</td>
<td>Unités de too8</td>
</tr>
<tr>
<td><strong>Ponts IAE par unité</strong></td>
<td>Non inclus</td>
<td>25</td>
<td>25</td>
<td>125</td>
<td>500</td>
</tr>
<tr>
<td><strong>EDI, AS2</strong>
<br/><br/>
Inclut les contrats TPM</td>
<td>Non inclus</td>
<td>Inclus. 10 contrats par unité.</td>
<td>Inclus. 50 contrats par unité.</td>
<td>Inclus. 250 contrats par unité.</td>
<td>Inclus. 1000 contrats par unité.</td>
</tr>
<tr>
<td><strong>Connexions hybrides par unité</strong></td>
<td>5</td>
<td>5</td>
<td>10</td>
<td>50</td>
<td>100</td>
</tr>
<tr>
<td><strong>Transfert de données des connexions hybrides (Go) par unité</strong></td>
<td>5</td>
<td>5</td>
<td>50</td>
<td>250</td>
<td>500</td>
</tr>
<tr>
<td><strong>Systèmes métier de Service d’adaptateur BizTalk connexions tooon local</strong></td>
<td>Non inclus</td>
<td>1 connexion</td>
<td>2 connexions</td>
<td>5 connexions</td>
<td>25 connexions</td>
</tr>
<tr>
<td align="left"><strong>Protocoles/systèmes pris en charge :</strong>
<ul>
<li>http</li>
<li>HTTPS</li>
<li>FTP</li>
<li>SFTP</li>
<li>WCF</li>
<li>Service Bus (SB)</li>
<li>Objets blob Azure</li>
<li>API REST</li>
</ul>
</td>
<td>Non inclus</td>
<td>Inclus</td>
<td>Inclus</td>
<td>Inclus</td>
<td>Inclus</td>
</tr>
<tr>
<td><strong>Haute disponibilité</strong>
<br/><br/>
Pour le contrat de niveau de service (SLA), consultez <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=304011"> Tarification Azure BizTalk Services</a>.
</td>
<td>Non inclus</td>
<td>Non inclus</td>
<td>Inclus</td>
<td>Inclus</td>
<td>Inclus</td>
</tr>
<tr>
<td><strong>Sauvegarde et restauration</strong></td>
<td>Non inclus</td>
<td>Inclus</td>
<td>Inclus</td>
<td>Inclus</td>
<td>Inclus</td>
</tr>
<tr>
<td><strong>Suivi</strong></td>
<td>Non inclus</td>
<td>Inclus</td>
<td>Inclus</td>
<td>Inclus</td>
<td>Inclus</td>
</tr>
<tr>
<td><strong>Archivage</strong><br/><br/>
Inclut NRR et le téléchargement des messages suivis</td>
<td>Non inclus</td>
<td>Inclus</td>
<td>Non inclus</td>
<td>Non inclus</td>
<td>Inclus</td>
</tr>
<tr>
<td><strong>Utilisation de code personnalisé</strong></td>
<td>Non inclus</td>
<td>Inclus</td>
<td>Inclus</td>
<td>Inclus</td>
<td>Inclus</td>
</tr>
<tr>
<td><strong>Utilisation des transformations, notamment la personnalisation XSLT</strong></td>
<td>Non inclus</td>
<td>Inclus</td>
<td>Inclus</td>
<td>Inclus</td>
<td>Inclus</td>
</tr>
</table>

> [!NOTE]
> Pour résister aux risques de pannes, la haute disponibilité nécessite plusieurs machines virtuelles dans une seule unité BizTalk.
> 
> 

## <a name="faqs"></a>FAQ
#### <a name="what-is-a-biztalk-unit"></a>Qu'est-ce qu'une unité BizTalk ?
« Unité » est atomique au niveau du hello d’un déploiement d’Azure BizTalk Services. Chaque édition est livrée avec une unité ayant différentes capacités de calcul et de mémoire. Par exemple, une unité De base comprend davantage d'ordinateurs qu'une unité Développeur, une unité Standard dispose d'une plus grande capacité de calcul qu'une unité De base, etc. Lorsque vous mettez à l'échelle un service BizTalk, cette mise à l'échelle s'effectue en termes d'unités.

#### <a name="what-is-hello-difference-between-biztalk-services-and-azure-biztalk-vm"></a>Qu’est la différence de hello entre les Services BizTalk et de la machine virtuelle de Azure BizTalk ?
BizTalk Services fournit une véritable architecture Platform-as-a-Service (PaaS) pour la création de solutions d’intégration dans le cloud de hello. Avec le modèle de PaaS hello, vous concentrer entièrement sur la logique d’application hello et laissez toutes les tooMicrosoft de gestion d’infrastructure de hello, y compris :

* Aucun besoin de toomanage ou correctif de machines virtuelles.
* Microsoft s'occupe de maintenir la disponibilité.
* Vous contrôlez l’échelle à la demande en simplement demandant plus ou moins la capacité via hello portail Azure.

BizTalk Server sur les machines virtuelles Azure fournit une architecture IaaS (Infrastructure-as-a-Service). Vous créez des ordinateurs virtuels et les configurer exactement comme votre environnement local, rendant les applications existantes toorun plus faciles dans le cloud hello sans aucune modification de code. Avec IaaS, vous êtes toujours responsable de la configuration des machines virtuelles de hello hello virtuels (par exemple, lors de l’installation des logiciels et des correctifs de système d’exploitation) et la gestion des architecture d’application hello pour la haute disponibilité.

Si vous voulez développer de nouvelles solutions d'intégration pour faciliter la gestion de votre architecture, choisissez BizTalk Services. Si vous cherchez tooquickly migrez vos solutions existantes de BizTalk ou recherchant une toodevelop de l’environnement de la demande et le test de BizTalk Server applications, utilisez BizTalk Server sur une Machine virtuelle de Azure.

#### <a name="what-is-hello-difference-between-biztalk-adapter-service-and-hybrid-connections"></a>Nouveautés différence hello entre le Service d’adaptateur BizTalk et de connexions hybrides
Hello Service d’adaptateur BizTalk est utilisé par un BizTalk Service de Azure. Hello Service d’adaptateur BizTalk utilise un système métier (LOB) de hello BizTalk Adapter Pack tooconnect tooan local. Une connexion hybride fournit un moyen simple et pratique de tooconnect des applications Azure, comme les applications Web hello dans Azure App Service et Azure Mobile Services tooan ressources sur site.

#### <a name="what-does-hybrid-connection-data-transfer-gb-per-unit-mean-is-this-per-minutehourdayweekmonth-what-happens-when-hello-limit-is-reached"></a>Qu’est-ce que le « Transfert de données des connexions hybrides (Go) par unité » ? Est-ce qu’il s’agit d’un transfert par minute/heure/jour/semaine/mois ? Que se passe-t-il lorsque hello limite est atteinte ?
Hello coût de la connexion hybride par unité dépend de l’édition de BizTalk Services hello. En bref, les coûts dépendent de la quantité de données que vous transférez. Par exemple, un transfert quotidien de 10 Go de données est moins cher qu'un transfert quotidien de 100 Go. Hello d’utilisation [calculatrice de tarification](https://azure.microsoft.com/pricing/calculator/?scenario=full) pour des coûts spécifiques de BizTalk Services toodetermine. En règle générale, les limites de hello sont appliquées tous les jours. Si vous dépassez la limite de hello, tout dépassement est facturée au taux de hello $ 1 Go.

#### <a name="when-i-create-an-agreement-in-biztalk-services-why-does-hello-number-of-bridges-go-up-by-two-instead-of-just-one"></a>Quand je crée un accord dans BizTalk Services, pourquoi nombre hello des ponts monter par deux au lieu d’un seul ?
Chaque contrat comprend deux ponts différents : un pont de communication pour l'envoi, et un autre pour la réception.

#### <a name="what-happens-when-i-hit-hello-quota-limit-on-hello-number-of-bridges-or-agreements"></a>Que se passe-t-il lorsque j’atteins hello quota hello nombre limite de contrats ou les ponts ?
Vous n’a pas pu toodeploy les ponts nouvelle ou créez de nouveaux contrats. toodeploy plus, vous devez tooscale unités toomore du service de BizTalk hello ou édition supérieure de tooa mise à niveau.

#### <a name="how-do-i-migrate-from-one-tier-of-biztalk-services-tooanother"></a>Comment migrer d’un niveau de BizTalk Services tooanother ?
édition gratuite de Hello ne peut pas être migré ou 'échelle' tooanother couche et ne peut pas être sauvegardée et restauré tooanother couche. Si vous avez besoin d’une autre couche, créer un nouveau BizTalk Service à l’aide du nouveau niveau de hello. Tous les artefacts créés à l’aide d’édition gratuite de hello, y compris les connexions hybrides toobe besoin recréé dans hello nouveau BizTalk Service. 

Pour les éditions restantes hello, utilisez hello sauvegarde et restauration de la migration de vos artefacts d’une couche tooanother. Par exemple, sauvegardez vos artefacts de niveau Standard de hello et restaurez-les niveau Premium de toohello. [Les Services BizTalk : Sauvegarde et restauration](biztalk-backup-restore.md) décrit les chemins de migration pris en charge de hello et répertorie les artefacts sont sauvegardés. Notez que les connexions hybrides ne sont pas sauvegardées. Après la sauvegarde et restauration des tooa nouvelle couche, vous recréez les connexions hybrides hello.  

#### <a name="is-hello-biztalk-adapter-service-included-in-hello-service-how-do-i-receive-hello-software"></a>Hello Service d’adaptateur BizTalk est inclus dans le service hello ? Comment recevoir des logiciels de hello ?
Oui, hello Service d’adaptateur BizTalk avec hello BizTalk Adapter Pack sont incluses avec hello Azure BizTalk Services SDK [télécharger](http://www.microsoft.com/download/details.aspx?id=39087).

## <a name="next-steps"></a>Étapes suivantes
toocreate Azure BizTalk Services dans hello Azure, accédez trop[BizTalk Services : approvisionnement à l’aide de hello Azure portal](biztalk-provision-services.md). toostart création d’applications, accédez trop[Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).

## <a name="additional-resources"></a>Ressources supplémentaires
* [Les Services BizTalk : Approvisionnement à l’aide de hello portail Azure](biztalk-provision-services.md)<br/>
* [Tableau comparatif des états d'approvisionnement BizTalk Services](biztalk-service-state-chart.md)<br/>
* [Onglets Tableau de bord, Surveiller et Mettre à l'échelle dans BizTalk Services](biztalk-dashboard-monitor-scale-tabs.md)<br/>
* [BizTalk Services: Backup and restore](biztalk-backup-restore.md)<br/>
* [Limitation dans BizTalk Services](biztalk-throttling-thresholds.md)<br/>
* [Nom et clé de l'émetteur dans BizTalk Services](biztalk-issuer-name-issuer-key.md)<br/>
* [Comment puis-je démarrer à l’aide de hello SDK des Services BizTalk Azure](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>

