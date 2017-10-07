---
title: "Fournisseurs et emplacements de connectivité : Azure ExpressRoute | Microsoft Docs"
description: "Cet article fournit une présentation détaillée des emplacements où les services sont proposés et comment tooconnect tooAzure régions. Trié par fournisseur de connectivité."
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
ms.assetid: c878513a-d594-42ad-8b0e-403efd0c4b25
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/17/2017
ms.author: kaanan
ms.openlocfilehash: df906ae6ff4e149c9cab4aa46ab78c8dd6aa4366
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-partners-and-peering-locations"></a>Partenaires ExpressRoute et emplacements d’homologation

> [!div class="op_single_selector"]
> * [Emplacements par fournisseur](expressroute-locations.md)
> * [Fournisseurs par emplacement](expressroute-locations-providers.md)


tables Hello dans cet article fournissent des informations sur les fournisseurs de connectivité ExpressRoute, ExpressRoute de couverture géographique, les services de cloud Microsoft pris en charge via ExpressRoute et ExpressRoute (intégrateurs système).

## <a name="partners"></a>Fournisseurs de connectivité ExpressRoute
ExpressRoute est pris en charge dans tous les emplacements et régions Azure. Hello suivant carte fournit une liste des régions Azure et les emplacements ExpressRoute. Les emplacements ExpressRoute font référence toothose où Microsoft homologues avec plusieurs fournisseurs de services.

![Carte des emplacements][0]

Vous aurez accès tooAzure services toutes les régions dans une région géopolitique si vous connecté tooat au moins un emplacement de ExpressRoute au sein de la région de hello géopolitiques.

### <a name="azure-regions-tooexpressroute-locations-within-a-geopolitical-region"></a>Emplacements des régions Azure tooExpressRoute dans une région géopolitique.
Hello tableau suivant fournit une liste des régions Azure emplacements tooExpressRoute dans une région géopolitique.

| **Région géopolitique** | **Régions Azure** | **Emplacements ExpressRoute** |
| --- | --- | --- |
| **Amérique du Nord** |Est des États-Unis, Ouest des États-Unis, Est des États-Unis 2, Ouest des États-Unis 2, Centre des États-Unis, Centre-Sud des États-Unis, Centre-Nord des États-Unis, Centre Ouest des États-Unis, Centre du Canada, Est du Canada |Atlanta, Chicago, Dallas, Denver, Las Vegas, Los Angeles, Miami, New York, San Antonio, Seattle, Silicon Valley, Washington DC, Montréal, Québec, Toronto |
| **Amérique du Sud** |Sud du Brésil |São Paulo |
| **Europe** |Europe du Nord, Europe de l’Ouest, Ouest du Royaume-Uni, Sud du Royaume-Uni |Amsterdam, Dublin, Londres, Newport (Pays de Galles), Paris |
| **Asie** |Asie orientale, Asie du Sud-Est |Hong Kong, Singapour |
| **Japon** |Ouest du Japon, Est du Japon |Osaka, Tokyo |
| **Australie** |Sud-est de l’Australie |Est de l’Australie |Melbourne, Sydney |
| **Inde** |Inde-Ouest, Inde-Centre, Inde-Sud |Chennai, Mumbai |
| **Corée du Sud** |Centre de la Corée, Corée du Sud |Busan, Séoul |

### <a name="regions-and-geopolitical-boundaries-for-national-clouds"></a>Régions et limites géopolitiques pour les clouds nationaux
tableau Hello ci-dessous fournit des informations sur les régions et des limites géopolitiques pour les clouds nationales.

| **Région géopolitique** | **Régions Azure** | **Emplacements ExpressRoute** |
| --- | --- | --- |
| **Cloud du gouvernement des États-Unis** |Gouvernement des États-Unis - Iowa, Gouvernement des États-Unis - Virginie, US DoD Centre, US DoD Est  |Chicago, Dallas, New York, Seattle, Silicon Valley, Washington DC |
| **Chine** |Chine du Nord, Chine orientale |Beijing, Shanghai |
| **Allemagne** |Allemagne centrale, Allemagne de l’est |Berlin, Francfort |

Connectivité entre les régions géopolitiques n’est pas pris en charge sur la norme de hello ExpressRoute SKU. Vous devez tooenable hello ExpressRoute premium module complémentaire toosupport connectivité globale. Environnements de cloud toonational connectivité n’est pas pris en charge. En cas de besoin, vous pouvez collaborer avec votre fournisseur de connectivité.

## <a name="locations"></a>Emplacements de fournisseur de connectivité

Hello tableau suivant indique les emplacements par le fournisseur de services. Si vous souhaitez tooview les fournisseurs disponibles par emplacement, consultez [fournisseurs par emplacement de Service](expressroute-locations-providers.md#locations).


### <a name="production-azure"></a>Production Azure
| **Fournisseur de services** | **Microsoft Azure** | **Office 365 et Dynamics 365** | **Emplacements** |
| --- | --- | --- | --- |
| **[AARNet](https://www.aarnet.edu.au/network-and-services/cloud-services-applications/azure-expressroute/)** |Pris en charge |Pris en charge |Melbourne, Sydney |
| **[Airtel](http://www.airtel.in/business/connexion)** | Pris en charge | Pris en charge | Chennai, Mumbai |
| **[Aryaka Networks](http://www.aryaka.com/)** |Pris en charge |Pris en charge |Amsterdam, Dallas, Hong Kong, Silicon Valley, Singapour, Tokyo, Washington DC |
| **[Ascenty Data Centers](https://ascenty.com/solucoes/conectividade-e-interconexoes/Microsoft-express-route/)** |Bientôt disponible |Bientôt disponible |São Paulo |
| **[AT&amp;T NetBond](https://www.synaptic.att.com/clouduser/html/productdetail/ATT_NetBond.htm)** |Pris en charge |Pris en charge |Amsterdam, Chicago, Dallas, Londres, Silicon Valley, Singapour, Sydney, Tokyo, Toronto, Washington DC |
| **[Bell Canada](https://business.bell.ca/shop/enterprise/cloud-connect-access-to-cloud-partner-services)** |Pris en charge |Pris en charge |Montréal, Toronto |
| **[British Telecom](http://www.globalservices.bt.com/uk/en/news/bt_to_provide_connectivity_to_microsoft_azure)** |Pris en charge |Pris en charge |Amsterdam, Hong Kong, Londres, Silicon Valley, Singapour, Sydney, Tokyo, Washington DC |
| **[CenturyLink](http://www.centurylink.com/business/enterprise/services/data-network/mpls-vpn.html)** |Bientôt disponible |Bientôt disponible |Silicon Valley |
| **China Telecom Global** |Pris en charge |Non pris en charge |Hong Kong |
| **[Cologix](http://www.cologix.com/solutions/cloud-connect/public-clouds/microsoft-cloud/)** |Pris en charge |Pris en charge |Dallas, Montréal, Toronto |
| **[Colt](http://www.colt.net/uk/en/news/colt-announces-dedicated-cloud-access-for-microsoft-azure-services-en.htm)** |Pris en charge |Pris en charge |Amsterdam, Dublin, Londres, Paris, Tokyo |
| **Comcast** |Pris en charge |Pris en charge |Chicago, Silicon Valley, Washington DC |
| **[Console](https://www.consoleconnect.com/partners/cloudsaas/)**| Pris en charge | Pris en charge |Silicon Valley, Toronto |
| **[CoreSite](http://www.coresite.com/solutions/cloud-services/public-cloud-providers/microsoft-azure-expressroute)** |Pris en charge |Pris en charge |Denver, Los Angeles, New York |
| **[Equinix](http://www.equinix.com/partners/microsoft-azure/)** |Pris en charge |Pris en charge |Amsterdam, Atlanta, Chicago, Dallas, Hong Kong, Londres, Los Angeles, Melbourne, New York, Osaka, Paris, Sao Paulo, Seattle, Silicon Valley, Singapour, Sydney, Tokyo, Toronto, Washington DC |
| **euNetworks** |Pris en charge |Pris en charge |Amsterdam |
| **GÉANT** |Pris en charge |Pris en charge |Amsterdam |
| **[Global Cloud Xchange (GCX)] (http://globalcloudxchange.com/cloud-platform/cloud-x-fusion/cloud-x-fusion-for-azure/)** | Pris en charge| Pris en charge | Chennai |
| **[InterCloud](https://www.intercloud.com/)** |Pris en charge |Pris en charge |Amsterdam, Londres, Singapour, Washington DC |
| **[Internet Initiative Japan Inc. - IIJ](http://www.iij.ad.jp/en/news/pressrelease/2015/1216-2.html)** |Pris en charge |Pris en charge |Osaka, Tokyo |
| **Internet Solutions - Cloud Connect** |Pris en charge |Pris en charge |Amsterdam, Londres |
| **[Interxion](http://www.interxion.com/why-interxion/colocate-with-the-clouds/Microsoft-Azure/)** |Pris en charge |Pris en charge |Amsterdam, Dublin, Londres, Paris |
| **Jisc** |Pris en charge |Pris en charge |Londres |
| **KINX** |Pris en charge |Pris en charge |Séoul |
| **[KPN](http://www.kpn.com/cloudconnect)** | Pris en charge | Pris en charge | Amsterdam | 
| **[Level 3 Communications](http://your.level3.com/LP=882?WT.tsrc=02192014LP882AzureVanityAzureText)** |Pris en charge |Pris en charge |Amsterdam, Chicago, Dallas, Las Vegas, Londres, São Paulo, Seattle, Silicon Valley, Singapour, Washington DC |
| **LG CNS** |Pris en charge |Pris en charge |Busan, Séoul |
| **[Megaport](https://www.megaport.com/services/microsoft-expressroute/)** |Pris en charge |Pris en charge |Amsterdam, Chicago, Dallas, Hong Kong, Las Vegas, Londres, Los Angeles, Melbourne, Miami, New York, Québec, San Antonio, Seattle, Silicon Valley, Singapour, Sydney, Toronto, Washington DC |
| **MTN** |Pris en charge |Pris en charge |Londres |
| **[Neutrona Networks](http://www.neutrona.com/index.php/services#cloud-connect)** |Pris en charge |Pris en charge |Miami, Sao Paulo |
| **[Next Generation Data](http://www.nextgenerationdata.co.uk/ngd-cloud-gateway/)** |Pris en charge |Pris en charge |Newport (Nouvelle-Galles du Sud) |
| **NEXTDC** |Pris en charge |Pris en charge |Melbourne, Sydney |
| **[NTT Communications](http://www.ntt.com/en/services/network/virtual-private-network.html)** |Pris en charge |Pris en charge |Londres, Los Angeles, Osaka, Singapour, Tokyo, Washington DC |
| **[NTT SmartConnect](http://cloud.nttsmc.com/cxc/azure.html)** |Pris en charge |Pris en charge |Osaka |
| **[Orange](http://www.orange-business.com/en/products/business-vpn-galerie)** |Pris en charge |Pris en charge |Amsterdam, Hong Kong, Londres, Paris, Silicon Valley, Singapour, Sydney, Washington DC |
| **PCCW Global Limited** |Pris en charge |Pris en charge |Hong Kong |
| **Sejong Telecom** |Pris en charge |Pris en charge |Séoul |
| **[SIFY](http://telecom.sify.com/azure-expressroute.html)** |Pris en charge |Pris en charge |Chennai |
| **[SingTel](http://info.singtel.com/about-us/news-releases/singtel-provide-secure-private-access-microsoft-azure-public-cloud)** |Pris en charge |Pris en charge |Singapour |
| **[Softbank](http://www.softbank.jp/biz/cloud/cloud_access/direct_access_for_az/)** |Pris en charge |Pris en charge |Osaka, Tokyo |
| **[Tata Communications](http://www.tatacommunications.com/lp/izo/azure/azure_index.html)** |Pris en charge |Pris en charge |Amsterdam, Chennai, Hong Kong, Londres, Mumbai, Silicon Valley, Singapour, Washington DC |
| **[TeleCity Group](http://www.telecitygroup.com/investor-centre/news_details.htm?locid=03100500400b00d&xml)** |Pris en charge |Pris en charge |Amsterdam, Dublin, Londres |
| **[Telefonica](https://www.business-solutions.telefonica.com/es/enterprise/solutions/efficient-infrastructure/managed-voice-data-connectivity/)** |Pris en charge |Pris en charge |Amsterdam, São Paulo |
| **[Telehouse - KDDI](http://www.telehouse.net/solutions/cloud-services/cloud-link)** |Pris en charge |Pris en charge |Londres |
| **Telenor** |Pris en charge |Pris en charge |Amsterdam, Londres |
| **[Telstra Corporation](http://www.telstra.com.au/business-enterprise/network-services/networks/cloud-direct-connect/)** |Pris en charge |Pris en charge |Melbourne, Sydney |
| **[Telus](http://www.telus.com)** |Pris en charge |Pris en charge |Toronto |
| **[UOLDIVEO](http://www.uoldiveo.com.br/solucoes/cloud.html#rmcl)** |Pris en charge |Pris en charge |São Paulo |
| **[Verizon](http://www.verizonenterprise.com/products/networking/secure-cloud-interconnect/)** |Pris en charge |Pris en charge |Amsterdam, Chicago, Dallas, Hong Kong, Londres, Silicon Valley, Singapour, Sydney, Tokyo, Washington DC |
| **[Vodafone](http://www.vodafone.com/business/global-enterprise/global-connectivity/vodafone-ip-vpn-cloud-connect)** |Pris en charge |Non pris en charge |Londres |
| **[Zayo Group](http://www.zayo.com/solutions/industries/cloud-connectivity/microsoft-expressroute)** |Pris en charge |Pris en charge |Amsterdam, Chicago, Dallas+, Londres+, Los Angeles, New York, Silicon Valley, Toronto, Washington DC |

 **+** = bientôt disponible

### <a name="national-cloud-environment"></a>Environnement de cloud national

### <a name="us-government-cloud"></a>Cloud du gouvernement des États-Unis
| **Fournisseur de services** | **Microsoft Azure** | **Office 365** | **Emplacements** |
| --- | --- | --- | --- |
| **[AT&amp;T NetBond](https://www.synaptic.att.com/clouduser/html/productdetail/ATT_NetBond.htm)** |Pris en charge |Pris en charge |Chicago, Washington DC |
| **[Equinix](http://www.equinix.com/partners/microsoft-azure/)** |Pris en charge |Pris en charge |Chicago, Dallas, New York, Seattle, Silicon Valley, Washington DC |
| **[Level 3 Communications](http://your.level3.com/LP=882?WT.tsrc=02192014LP882AzureVanityAzureText)** |Pris en charge |Pris en charge |Chicago, New York+, Silicon Valley, Washington DC |
| **[Megaport](https://www.megaport.com/services/microsoft-expressroute/)** |Pris en charge | Pris en charge | Chicago, Dallas |
| **[Verizon](http://news.verizonenterprise.com/2014/04/secure-cloud-interconnect-solutions-enterprise/)** |Pris en charge |Pris en charge |Chicago, Dallas, New York, Washington DC |

### <a name="china"></a>Chine
| **Fournisseur de services** | **Microsoft Azure** | **Office 365** | **Emplacements** |
| --- | --- | --- | --- |
| **China Telecom** |Pris en charge |Non pris en charge |Beijing, Shanghai |

toolearn, voir [ExpressRoute en Chine](http://www.windowsazure.cn/home/features/expressroute/).

### <a name="germany"></a>Allemagne
| **Fournisseur de services** | **Microsoft Azure** | **Office 365** | **Emplacements** |
| --- | --- | --- | --- |
| **[Colt](http://www.colt.net/uk/en/news/colt-announces-dedicated-cloud-access-for-microsoft-azure-services-en.htm)** |Pris en charge |Non pris en charge |Berlin+, Francfort |
| **[Equinix](http://www.equinix.com/partners/microsoft-azure/)** |Pris en charge |Non pris en charge |Francfort |
| **[e-shelter](https://www.e-shelter.de/en/microsoft-expressroutetm)** |Pris en charge |Non pris en charge |Berlin |
| **Interxion** |Pris en charge |Non pris en charge |Francfort |
| **[Megaport](https://www.megaport.com/services/microsoft-expressroute/)** |Pris en charge  | Non pris en charge | Berlin |
| **T-Systems** |Pris en charge |Non pris en charge |Berlin |

## <a name="connectivity-through-exchange-providers"></a>Connectivité via des fournisseurs Exchange

Si votre fournisseur de connectivité ne se trouve pas dans la liste des sections précédentes, vous pouvez quand même créer une connexion.

* Vérifiez auprès de votre toosee de fournisseur de connectivité s’ils sont connecté tooany d’échanges hello dans la table hello ci-dessus. Vous pouvez vérifier les liens suivants de hello de toogather de plus d’informations sur les services proposés par les fournisseurs exchange. Plusieurs fournisseurs de connectivité sont déjà connectés tooEthernet échanges.
  * [Cologix](http://www.cologix.com/)
  * [Console](https://www.consoleconnect.com/partners/cloudsaas/)
  * [CoreSite](http://www.coresite.com/)
  * [Equinix Cloud Exchange](http://www.equinix.com/services/interconnection-connectivity/cloud-exchange/)
  * [Interxion](http://www.interxion.com/products/interconnection/cloud-connect/)
  * [Megaport](https://www.megaport.com/services/microsoft-expressroute/)
  * [NextDC](http://www.nextdc.com/)
  * [TeleCity CloudIX](http://www.telecitygroup.com/colocation-services/cloud-ix.htm)
* Avoir votre fournisseur de connectivité étendre votre emplacement d’homologation toohello de réseau de choix.
  * Vérifiez que votre fournisseur de connectivité étend votre connectivité avec une haute disponibilité pour éviter tout point de défaillance unique.
* Commander un circuit ExpressRoute avec exchange de hello en tant que votre fournisseur de connectivité tooconnect tooMicrosoft.
  * Suivez les étapes de [créer un circuit ExpressRoute](expressroute-howto-circuit-classic.md) tooset la connectivité.

## <a name="connectivity-through-additional-service-providers"></a>Connectivité via d’autres fournisseurs de services

| **Fournisseur de connectivité** | **Microsoft Exchange** | **Emplacements** |
| --- | --- | --- |
| **[1CLOUDSTAR](http://www.1cloudstar.com/service/cloudconnect-azure-expressroute/)** |Equinix |Singapour |
| **[Airgate Technologies, Inc.](http://airgate.ca/cloud-express/)** | Equinix, Cologix | Toronto, Montréal |
| **[Alaska Communications](http://www.alaskacommunications.com/For-Your-Business/Direct-Cloud-Service)** |Equinix |Seattle |
| **[Altice Business](https://golightpath.com/transport)** |Equinix |New York, Washington DC |
| **[Arteria Networks Corporation](https://arteria-net.com/business/service/cloud_access/sca/)** |Equinix |Tokyo |
| **[Bezeq International Ltd.](https://www.bezeqint.net/english)** | euNetworks | Londres |
| **[BroadBand Tower, Inc.](http://www.bbtower.co.jp/product-service/data-center/network/dcconnect-for-azure/)** | Equinix | Tokyo |
| **[C3ntro Telecom](http://www.c3ntro.com/data/cloud-conectivity/)** | Equinix, Megaport | Dallas |
| **[Cogeco Peer 1](https://www.cogecopeer1.com/en/)**| Equinix | Montréal, Toronto |
| **[Cox Business](https://www.cox.com/business/networking/cloud-connectivity.html)** | Equinix | Dallas, Silicon Valley, Washington DC | 
| **[Data Foundry](https://www.datafoundry.com/services/cloud-connect)** | Megaport | Dallas |
| **[Epsilon Telecommunications Limited](http://www.epsilontel.com/data-connectivity/cloud-access/)** | Equinix | Londres, Singapour, Washington DC |
| **[Eurofiber](https://eurofiber.nl/microsoft-azure/)** | Equinix | Amsterdam |
| **[Exponential E](http://www.exponential-e.com/services/connectivity-services/cloud-connect-exchange)** | Equinix | Londres |
| **[Fastweb S.p.A](http://www.fastweb.it/grandi-aziende/connessione-voce-e-wifi/scheda-prodotto/rete-privata-virtuale/)** | Equinix | Amsterdam |
| **[Gtt Communications Inc](https://www.gtt.net/wp-content/uploads/2017/04/EtherCloud-Data-Sheet.pdf)** |Equinix | Washington DC |
| **[HSO](http://www.hso.co.uk/products/cloud-direct)** |Equinix | Londres, Slough |
| **LGA Telecom** |Equinix |Singapour|
| **[Lightower](http://www.lightower.com/network-solutions/cloud-connect/#microsoft-azure)** |Equinix | Chicago, New York, Washington DC |
| **[Macroview Telecom](http://www.macroview.com/en/scripts/catitem.php?catid=solution&sectionid=expressroute)** |Equinix |Hong Kong |
| **[Macquarie Telecom Group](https://macquariegovernment.com/secure-cloud/secure-cloud-exchange/)** | Megaport | Sydney |
| **[Masergy](https://www.masergy.com/solutions/hybrid-networking/cloud-marketplace/microsoft-azure)** | Equinix | Washington DC |
| **[NextGen Networks](http://www.nexgen-net.com/nexgen-networks-direct-connect-microsoft-azure-expressroute.html)** | Interxion | Londres |
| **[Nianet](https://nianet.dk/produkter/internet/microsoft-expressroute)** |Telecity | Amsterdam, Frankfort |  
| **[QSC AG](https://www.qsc.de/de/produkte-loesungen/cloud-services-und-it-outsourcing/pure-enterprise-cloud/multi-cloud-management/azure-expressroute/)** |Interxion | Francfort |  
| **Rogers** | Cologix, Equinix | Montréal, Toronto |
| **[Tamares Telecom](http://www.tamarestelecom.com/our-services/#Connectivity)** | Telecity | Londres | 
| **[ThinkTel](http://www.thinktel.ca/services/agile-ix-data/expressroute/)** | Equinix | Toronto | 
| **[Transtelco](http://www.transtelco.net/tcloud/microsoft)** |Equinix | Dallas, Los Angeles |  
| **[United Information Highway (UIH)](https://www.uih.co.th/en/internet-solution/cloud-direct/uih-cloud-direct-for-microsoft-azure-expressroute)**| Equinix | Singapour |
| **[Webair](https://www.webair.com/microsoft-express-route-partnership/)**| Megaport | New York |
| **[Windstream](http://www.windstreambusiness.com/solutions/cloud-services/cloud-and-managed-hosting-services)**| Equinix | Chicago, Silicon Valley, Washington DC |
| **Zain** |Equinix |Londres|
| **[Zertia](http://www.zertia.es/index.php/novedades)**| Niveau 3 | Madrid |
| **[Zirro](https://zirro.com/services/)**| Equinix | Montréal, Toronto |

## <a name="connectivity-through-datacenter-providers"></a>Connectivité via des fournisseurs de centres de données
| **Fournisseur** | **Microsoft Exchange** |
| --- | --- |
| **[Cyrus One](https://cyrusone.com/enterprise-data-center-services/connectivity-and-interconnection/cloud-connectivity-reaching-amazon-microsoft-google-and-more/microsoft-azure-expressroute/?doing_wp_cron=1498512235.6733090877532958984375)** | Megaport |
| **[Digital Realty](https://www.digitalrealty.com/services/interconnection/service-exchange/)** | Megaport |
| **[EdgeConnex](http://www.edgeconnex.com/services/edge-data-centers-proximity-matters/)** | Megaport |
| **[RagingWire Data Centers](http://www.ragingwire.com/wholesale/wholesale-data-centers-worldwide-nexcenters)** | Console |
| **[T5 Datacenters](http://t5datacenters.com/network-cloud-connect/)** | Console |

## <a name="connectivity-through-national-research-and-education-networks-nren"></a>Connectivité via les réseaux nationaux de la recherche et de l’enseignement (NREN)

| **Fournisseur**|
| --- |
| **AARNET**| 
| **DeIC, via GÉANT**|
| **GARR, via GÉANT**|
| **GÉANT**|
| **HEAnet, via GÉANT**|
| **JISC**|
| **RedIRIS, via GÉANT**|
| **SINET**|
| **Surfnet, via GÉANT**|

* Si votre fournisseur de connectivité n’est pas répertorié ici, consultez toosee s’ils sont connecté tooany Hello Qu'expressroute Exchange partenaires répertoriés ci-dessus.

## <a name="expressroute-system-integrators"></a>Intégrateurs système ExpressRoute
L’activation toofit connectivité privée que vos besoins peuvent être difficile, en fonction de l’échelle hello de votre réseau. Vous pouvez travailler avec des intégrateurs hello répertoriés dans hello suivant table tooassist vous avec d’intégration tooExpressRoute.

| **Intégrateur système** | **Continent** |
| --- | --- |
| **[Altogee](http://www.altogee.be/expressroute)** | Europe |
| **[Avanade Inc.](http://www.avanade.com/)** | Asie, Europe, Amérique du Nord, Amérique du Sud |
| **[Bright Skies GmbH](http://bskies.io/expressroute)** | Europe
| **[Ensyst](http://www.ensyst.com.au)** | Asie
| **[Equinix Professional Services](http://www.equinix.com/services/consulting/)** | Amérique du Nord |
| **[FlexManage](http://www.flexmanage.com/cloud)** | Amérique du Nord |
| **[Inframon](http://www.inframon.com/partner/microsoft/)** | Europe |
| **[Hello groupe de services de conseil informatique](http://itconsult.com.au/microsoft-expressroute)** | Australie |
| **[MOQdigital](http://www.moqdigital.com.au/insights/technical/network-connectivity-options-for-azure)** | Australie |
| **[MSG Services](https://www.msg-services.de/it-services/managed-services/cloud-outsourcing/)** | Europe (Allemagne) |
| **[Nelite](http://nelite.com/)** | Europe |
| **[New Signature](https://www.newsignature.co.uk/)** | Europe |
| **[OneAs1a](http://www.oneas1a.com/express-connect-any-cloud-ecac)** | Asie |
| **[Orange Networks](https://orange-networks.com/blog/88-azureexpressroute)** | Europe |
| **[Perficient](http://www.perficient.com/Partners/Microsoft/Cloud/Azure-ExpressRoute)** | Amérique du Nord |
| **[Presidio](http://info.presidio.com/microsoft-azure-expressroute)** | Amérique du Nord |
| **[sol-tec](http://www.sol-tec.com/Technologies)** | Europe |
| **[Vigilant.IT](https://vigilant.it/expressroute)** | Australie |


## <a name="next-steps"></a>Étapes suivantes
* Pour plus d’informations sur ExpressRoute, consultez hello [FAQ sur ExpressRoute](expressroute-faqs.md).
* Assurez-vous que toutes les conditions préalables sont remplies. Consultez la page [Configuration requise pour ExpressRoute](expressroute-prerequisites.md).

<!--Image References-->
[0]: ./media/expressroute-locations/expressroute-locations-map.png "Carte géographique"
