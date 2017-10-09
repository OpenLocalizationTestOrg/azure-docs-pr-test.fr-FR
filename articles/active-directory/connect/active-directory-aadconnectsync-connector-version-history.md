---
title: "historique des versions d’aaaConnector | Documents Microsoft"
description: "Cette rubrique répertorie toutes les versions de connecteurs de hello pour Forefront Identity Manager (FIM) et Microsoft Identity Manager (MIM)"
services: active-directory
documentationcenter: 
author: fimguy
manager: femila
editor: 
ms.assetid: 6a0c66ab-55df-4669-a0c7-1fe1a091a7f9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: fimguy
ms.openlocfilehash: 3522f17c30e46542eaa367ecdefdfd2fc47f71a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connector-version-release-history"></a><span data-ttu-id="11860-103">Historique de publication des versions du connecteur</span><span class="sxs-lookup"><span data-stu-id="11860-103">Connector Version Release History</span></span>
<span data-ttu-id="11860-104">Connecteurs Hello pour Forefront Identity Manager (FIM) et Microsoft Identity Manager (MIM) sont fréquemment mis à jour.</span><span class="sxs-lookup"><span data-stu-id="11860-104">hello Connectors for Forefront Identity Manager (FIM) and Microsoft Identity Manager (MIM) are updated frequently.</span></span>

> [!NOTE]
> <span data-ttu-id="11860-105">Cette rubrique ne concerne que FIM et MIM.</span><span class="sxs-lookup"><span data-stu-id="11860-105">This topic is on FIM and MIM only.</span></span> <span data-ttu-id="11860-106">Ces connecteurs ne sont pas pris en charge pour l’installation sur Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="11860-106">These Connectors are not supported for install on Azure AD Connect.</span></span> <span data-ttu-id="11860-107">Connecteurs finales sont préinstallés sur AADConnect toospecified Build de la mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="11860-107">Released Connectors are preinstalled on AADConnect when upgrading toospecified Build.</span></span>

<span data-ttu-id="11860-108">Cette rubrique répertorie toutes les versions de hello connecteurs qui ont été publiées.</span><span class="sxs-lookup"><span data-stu-id="11860-108">This topic list all versions of hello Connectors that have been released.</span></span>

<span data-ttu-id="11860-109">Liens connexes :</span><span class="sxs-lookup"><span data-stu-id="11860-109">Related links:</span></span>

* [<span data-ttu-id="11860-110">Télécharger les derniers connecteurs</span><span class="sxs-lookup"><span data-stu-id="11860-110">Download Latest Connectors</span></span>](http://go.microsoft.com/fwlink/?LinkId=717495)
* <span data-ttu-id="11860-111">[connecteur LDAP générique](active-directory-aadconnectsync-connector-genericldap.md)</span><span class="sxs-lookup"><span data-stu-id="11860-111">[Generic LDAP Connector](active-directory-aadconnectsync-connector-genericldap.md) reference documentation</span></span>
* <span data-ttu-id="11860-112">[connecteur SQL générique](active-directory-aadconnectsync-connector-genericsql.md)</span><span class="sxs-lookup"><span data-stu-id="11860-112">[Generic SQL Connector](active-directory-aadconnectsync-connector-genericsql.md) reference documentation</span></span>
* <span data-ttu-id="11860-113">[connecteur WebServices](http://go.microsoft.com/fwlink/?LinkID=226245)</span><span class="sxs-lookup"><span data-stu-id="11860-113">[Web Services Connector](http://go.microsoft.com/fwlink/?LinkID=226245) reference documentation</span></span>
* <span data-ttu-id="11860-114">[connecteur PowerShell](active-directory-aadconnectsync-connector-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="11860-114">[PowerShell Connector](active-directory-aadconnectsync-connector-powershell.md) reference documentation</span></span>
* <span data-ttu-id="11860-115">[connecteur Lotus Domino](active-directory-aadconnectsync-connector-domino.md)</span><span class="sxs-lookup"><span data-stu-id="11860-115">[Lotus Domino Connector](active-directory-aadconnectsync-connector-domino.md) reference documentation</span></span>


## <a name="116040-aadconnect-pending-release"></a><span data-ttu-id="11860-116">1.1.604.0 (AADConnect en attente de publication)</span><span class="sxs-lookup"><span data-stu-id="11860-116">1.1.604.0 (AADConnect Pending Release)</span></span>


### <a name="fixed-issues"></a><span data-ttu-id="11860-117">Problèmes résolus :</span><span class="sxs-lookup"><span data-stu-id="11860-117">Fixed issues:</span></span>

* <span data-ttu-id="11860-118">Services web génériques :</span><span class="sxs-lookup"><span data-stu-id="11860-118">Generic Web Services:</span></span>
  * <span data-ttu-id="11860-119">Correction d’un problème empêchant la création d’un projet SOAP lorsqu’il existait deux points de terminaison ou plus.</span><span class="sxs-lookup"><span data-stu-id="11860-119">Fixed an issue preventing a SOAP project from being created when there were two or more endpoints.</span></span>
* <span data-ttu-id="11860-120">SQL générique :</span><span class="sxs-lookup"><span data-stu-id="11860-120">Generic SQL:</span></span>
  * <span data-ttu-id="11860-121">Dans l’opération d’importation de hello hello GSQL a été pas conversion de l’heure correctement, quand enregistré tooconnector espace.</span><span class="sxs-lookup"><span data-stu-id="11860-121">In hello operation of import hello GSQL was not converting time correctly, when saved tooconnector space.</span></span> <span data-ttu-id="11860-122">format de date et d’heure par défaut pour l’espace de connecteur de hello GSQL Hello a été remplacé par 'AAAA-MM-JJ : ssZ' too'yyyy-MM-JJ : ssZ '.</span><span class="sxs-lookup"><span data-stu-id="11860-122">hello default date and time format for connector space of hello GSQL was changed from 'yyyy-MM-dd hh:mm:ssZ' too'yyyy-MM-dd HH:mm:ssZ'.</span></span>

## <a name="115510-aadconnect-115530"></a><span data-ttu-id="11860-123">1.1.551.0 (AADConnect 1.1.553.0)</span><span class="sxs-lookup"><span data-stu-id="11860-123">1.1.551.0 (AADConnect 1.1.553.0)</span></span>

### <a name="fixed-issues"></a><span data-ttu-id="11860-124">Problèmes résolus :</span><span class="sxs-lookup"><span data-stu-id="11860-124">Fixed issues:</span></span>

* <span data-ttu-id="11860-125">Services web génériques :</span><span class="sxs-lookup"><span data-stu-id="11860-125">Generic Web Services:</span></span>
  * <span data-ttu-id="11860-126">outil de Wsconfig Hello ne n’a pas converti correctement tableau Json de hello à partir de « exemple de demande » pour la méthode de service REST hello.</span><span class="sxs-lookup"><span data-stu-id="11860-126">hello Wsconfig tool did not convert correctly hello Json array from "sample request" for hello REST service method.</span></span> <span data-ttu-id="11860-127">Cela a provoqué des problèmes avec la sérialisation ce tableau Json pour la demande REST hello.</span><span class="sxs-lookup"><span data-stu-id="11860-127">This caused problems with serialization this Json array for hello REST request.</span></span>
  * <span data-ttu-id="11860-128">L’outil de configuration du connecteur de service web ne prend pas en charge l’utilisation de symboles d’espace dans les noms d’attribut JSON</span><span class="sxs-lookup"><span data-stu-id="11860-128">Web Service Connector Configuration Tool does not support usage of space symbols in JSON attribute names</span></span> 
    * <span data-ttu-id="11860-129">Un modèle de Substitution peut être ajouté manuellement toohello WSConfigTool.exe.config fichier, par exemple```<appSettings> <add key=”JSONSpaceNamePattern” value="__" /> </appSettings>```</span><span class="sxs-lookup"><span data-stu-id="11860-129">A Substitution pattern can be added manually toohello WSConfigTool.exe.config file, e.g. ```<appSettings> <add key=”JSONSpaceNamePattern” value="__" /> </appSettings>```</span></span>

* <span data-ttu-id="11860-130">Lotus Notes :</span><span class="sxs-lookup"><span data-stu-id="11860-130">Lotus Notes:</span></span>
  * <span data-ttu-id="11860-131">Lorsque hello option **autoriser certificateurs personnalisés pour les unités d’organisation/organisation** est désactivée puis échoue de connecteur hello lors de l’exportation (mise à jour) après l’exportation de hello transmet tous les attributs est exportée tooDomino mais au moment de hello de exportation KeyNotFoundException est retournée tooSync.</span><span class="sxs-lookup"><span data-stu-id="11860-131">When hello option **Allow custom certifiers for Organization/Organizational Units** is disabled then hello connector fails during export (Update) After hello export flow all attributes are exported tooDomino but at hello time of export a KeyNotFoundException is returned tooSync.</span></span> 
    * <span data-ttu-id="11860-132">Cela se produit car hello renommer échoue lorsqu’il tente toochange DN (attribut de nom d’utilisateur) en modifiant un des attributs hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="11860-132">This happens because hello rename operation fails when it tries toochange DN (UserName attribute) by changing one of hello attributes below:</span></span>  
      - <span data-ttu-id="11860-133">LastName</span><span class="sxs-lookup"><span data-stu-id="11860-133">LastName</span></span>
      - <span data-ttu-id="11860-134">FirstName</span><span class="sxs-lookup"><span data-stu-id="11860-134">FirstName</span></span>
      - <span data-ttu-id="11860-135">MiddleInitial</span><span class="sxs-lookup"><span data-stu-id="11860-135">MiddleInitial</span></span>
      - <span data-ttu-id="11860-136">AltFullName</span><span class="sxs-lookup"><span data-stu-id="11860-136">AltFullName</span></span>
      - <span data-ttu-id="11860-137">AltFullNameLanguage</span><span class="sxs-lookup"><span data-stu-id="11860-137">AltFullNameLanguage</span></span>
      - <span data-ttu-id="11860-138">Unité d’organisation</span><span class="sxs-lookup"><span data-stu-id="11860-138">ou</span></span>
      - <span data-ttu-id="11860-139">altcommonname</span><span class="sxs-lookup"><span data-stu-id="11860-139">altcommonname</span></span>

  * <span data-ttu-id="11860-140">Quand l’option **Allow custom certifiers for Organization/Organizational Units** (Autoriser les certificateurs personnalisés pour les organisations/unités d’organisation) est activée, mais que les certificateurs nécessaires sont encore vides, une exception KeyNotFoundException se produit.</span><span class="sxs-lookup"><span data-stu-id="11860-140">When **Allow custom certifiers for Organization/Organizational Units** option is enabled, but required certifiers are still empty, then KeyNotFoundException occurs.</span></span>

### <a name="enhancements"></a><span data-ttu-id="11860-141">Améliorations :</span><span class="sxs-lookup"><span data-stu-id="11860-141">Enhancements:</span></span>

* <span data-ttu-id="11860-142">SQL générique :</span><span class="sxs-lookup"><span data-stu-id="11860-142">Generic SQL:</span></span>
  * <span data-ttu-id="11860-143">**Scénario : repensé Implémenté  : fonctionnalité**  « * »</span><span class="sxs-lookup"><span data-stu-id="11860-143">**Scenario: redesigned Implemented:** "*" feature</span></span>
  * <span data-ttu-id="11860-144">**Description de la solution :** modification de l’approche pour la [gestion des attributs de référence à valeurs multiples](active-directory-aadconnectsync-connector-genericsql.md).</span><span class="sxs-lookup"><span data-stu-id="11860-144">**Solution description:** Changed approach for [multi-valued reference attributes handling](active-directory-aadconnectsync-connector-genericsql.md).</span></span>


### <a name="fixed-issues"></a><span data-ttu-id="11860-145">Problèmes résolus :</span><span class="sxs-lookup"><span data-stu-id="11860-145">Fixed issues:</span></span>

* <span data-ttu-id="11860-146">Services web génériques :</span><span class="sxs-lookup"><span data-stu-id="11860-146">Generic Web Services:</span></span>
  * <span data-ttu-id="11860-147">Impossible d’importer la configuration serveur si le connecteur de service web est présent</span><span class="sxs-lookup"><span data-stu-id="11860-147">Can’t import Server configuration if WebService Connector is present</span></span>
  * <span data-ttu-id="11860-148">Le connecteur de service web ne fonctionne pas avec plusieurs services web</span><span class="sxs-lookup"><span data-stu-id="11860-148">WebService Connector is not working with multiple  Web Services</span></span>

* <span data-ttu-id="11860-149">SQL générique :</span><span class="sxs-lookup"><span data-stu-id="11860-149">Generic SQL:</span></span>
  * <span data-ttu-id="11860-150">Aucun type d’objet n’est répertorié pour l’attribut référencé à valeur unique</span><span class="sxs-lookup"><span data-stu-id="11860-150">No object types are listed for single value referenced attribute</span></span>
  * <span data-ttu-id="11860-151">L’importation différentielle sur la stratégie Change Tracking supprime objet lorsque la valeur est supprimée de la table à valeurs multiples</span><span class="sxs-lookup"><span data-stu-id="11860-151">Delta import on Change Tracking strategy deletes object when value is removed from multi-value table</span></span>
  * <span data-ttu-id="11860-152">OverflowException dans le connecteur GSQL avec DB2 sur AS/400</span><span class="sxs-lookup"><span data-stu-id="11860-152">OverflowException in GSQL connector with DB2 on AS/400</span></span>

<span data-ttu-id="11860-153">Lotus :</span><span class="sxs-lookup"><span data-stu-id="11860-153">Lotus:</span></span>
  * <span data-ttu-id="11860-154">Tooenable\disable d’ajout de l’option recherche des unités d’organisation avant d’ouvrir la page de GlobalParameters</span><span class="sxs-lookup"><span data-stu-id="11860-154">Added option tooenable\disable searching OUs before opening GlobalParameters page</span></span>

## <a name="114430"></a><span data-ttu-id="11860-155">1.1.443.0</span><span class="sxs-lookup"><span data-stu-id="11860-155">1.1.443.0</span></span>

<span data-ttu-id="11860-156">Publié : mars 2017</span><span class="sxs-lookup"><span data-stu-id="11860-156">Released: 2017 March</span></span>

### <a name="enhancements"></a><span data-ttu-id="11860-157">Améliorations</span><span class="sxs-lookup"><span data-stu-id="11860-157">Enhancements</span></span>

* <span data-ttu-id="11860-158">SQL générique :</span><span class="sxs-lookup"><span data-stu-id="11860-158">Generic SQL:</span></span></br><span data-ttu-id="11860-159">
  **Scénario symptômes :** il s’agit d’une limitation connue de hello connecteur SQL où nous uniquement un type référence d’objet tooone et obligent référence croisée avec des membres.</span><span class="sxs-lookup"><span data-stu-id="11860-159">
  **Scenario Symptoms:**  It is a well-known limitation with hello SQL Connector where we only allow a reference tooone object type and require cross reference with members.</span></span> </br><span data-ttu-id="11860-160">
**Description de la solution :** à l’étape de traitement hello pour les références ont été « * » option est sélectionnée, toutes les combinaisons de types d’objet seront affichera comme moteur de synchronisation toohello précédent.</span><span class="sxs-lookup"><span data-stu-id="11860-160">
**Solution description:** In hello processing step for references were "*" option is chosen, ALL combinations of object types will be returned back toohello sync engine.</span></span>

>[!Important]
- <span data-ttu-id="11860-161">Cela crée de nombreux espaces réservés.</span><span class="sxs-lookup"><span data-stu-id="11860-161">This will create many placeholders</span></span>
- <span data-ttu-id="11860-162">Il est requis toomake que hello d’affectation de noms est unique entre les types d’objets.</span><span class="sxs-lookup"><span data-stu-id="11860-162">It is required toomake sure hello naming is unique cross object types.</span></span>


* <span data-ttu-id="11860-163">LDAP générique :</span><span class="sxs-lookup"><span data-stu-id="11860-163">Generic LDAP:</span></span></br><span data-ttu-id="11860-164">
 **Scénario :** lorsque que certains conteneurs sont sélectionnées dans une partition spécifique, puis recherche de hello toujours s’effectue dans une partition entière.</span><span class="sxs-lookup"><span data-stu-id="11860-164">
**Scenario:** When only few containers are selected in specific partition, then hello search still will be done in whole partition.</span></span> <span data-ttu-id="11860-165">La partition spécifique est filtrée par le service de synchronisation et non par MA, ce qui peut entraîner une dégradation des performances.</span><span class="sxs-lookup"><span data-stu-id="11860-165">Specific will be filtered by Synchronization Service, but not by MA which might cause performance degradation.</span></span> </br>

 <span data-ttu-id="11860-166">**Description de la solution :** toomake de code du connecteur GLDAP de modifié il est possible de passer par tous les conteneurs et rechercher des objets dans chacune d’elles, au lieu de rechercher dans la partition de toute hello.</span><span class="sxs-lookup"><span data-stu-id="11860-166">**Solution description:** Changed GLDAP connector's code toomake it possible go through all containers and search objects in each of them, instead of searching in hello whole partition.</span></span>


* <span data-ttu-id="11860-167">Lotus Domino :</span><span class="sxs-lookup"><span data-stu-id="11860-167">Lotus Domino:</span></span>

  <span data-ttu-id="11860-168">**Scénario :** Prise en charge de la suppression d’un courrier Domino pour la suppression d’une personne pendant une exportation.</span><span class="sxs-lookup"><span data-stu-id="11860-168">**Scenario:** Domino mail deletion support for a person removal during an export.</span></span> </br><span data-ttu-id="11860-169">
  **Solution :** Prise en charge de la suppression d’un courrier configurable pour la suppression d’une personne pendant une exportation.</span><span class="sxs-lookup"><span data-stu-id="11860-169">
**Solution:** Configurable mail deletion support for a person removal during an export.</span></span>

### <a name="fixed-issues"></a><span data-ttu-id="11860-170">Problèmes résolus :</span><span class="sxs-lookup"><span data-stu-id="11860-170">Fixed issues:</span></span>
* <span data-ttu-id="11860-171">Services web génériques :</span><span class="sxs-lookup"><span data-stu-id="11860-171">Generic Web Services:</span></span>
 * <span data-ttu-id="11860-172">Lors de la modification par défaut des URL du service hello SAP wsconfig projets via l’outil de Configuration de service Web puis hello l’erreur suivante se produit : Impossible de trouver une partie du chemin d’accès de hello</span><span class="sxs-lookup"><span data-stu-id="11860-172">When changing hello service URL in Default SAP wsconfig projects through WebService Configuration Tool then hello following error happens: Could not find a part of hello path</span></span>

      ``'C:\Users\cstpopovaz\AppData\Local\Temp\2\e2c9d9b0-0d8a-4409-b059-dceeb900a2b3\b9bedcc0-88ac-454c-8c69-7d6ea1c41d17\cfg.config\cloneconfig.xml'. ``

* <span data-ttu-id="11860-173">LDAP générique :</span><span class="sxs-lookup"><span data-stu-id="11860-173">Generic LDAP:</span></span>
 * <span data-ttu-id="11860-174">Le connecteur GLDAP ne voit pas tous les attributs dans AD LDS</span><span class="sxs-lookup"><span data-stu-id="11860-174">GLDAP Connector does not see all attributes in AD LDS</span></span>
 * <span data-ttu-id="11860-175">Assistant sauts lorsqu’aucun attribut UPN n’est détectées dans le schéma d’annuaire LDAP hello</span><span class="sxs-lookup"><span data-stu-id="11860-175">Wizard breaks when no UPN attributes are detected from hello LDAP directory schema</span></span>
 * <span data-ttu-id="11860-176">Les échecs d’importation delta avec erreurs de détection n’apparaissent pas pendant l’importation complète, lorsque l’attribut « objectclass » n’est pas sélectionné.</span><span class="sxs-lookup"><span data-stu-id="11860-176">Delta Imports Failing with discovery errors not present during full import, when "objectclass" attribute is not selected</span></span>
 * <span data-ttu-id="11860-177">Une page de configuration « Configurer des Partitions et des hiérarchies », n’affiche pas tous les objets que le type est partition toohello égal pour les nouveaux serveurs Bonjour générique</span><span class="sxs-lookup"><span data-stu-id="11860-177">A "Configure Partitions and Hierarchies” configuration page, doesn’t show any objects which type is equal toohello partition for Novel servers in hello Generic</span></span>  
<span data-ttu-id="11860-178">générique.</span><span class="sxs-lookup"><span data-stu-id="11860-178">LDAP MA.</span></span> <span data-ttu-id="11860-179">Seuls les objets de la partition RootDSE sont affichés.</span><span class="sxs-lookup"><span data-stu-id="11860-179">They showed only objects from RootDSE partition.</span></span>


* <span data-ttu-id="11860-180">SQL générique :</span><span class="sxs-lookup"><span data-stu-id="11860-180">Generic SQL:</span></span>
 * <span data-ttu-id="11860-181">Correction du bogue empêchant l’importation d’un attribut à valeurs multiples d’importation delta de filigrane SQL générique</span><span class="sxs-lookup"><span data-stu-id="11860-181">Fix for Generic SQL watermark Delta Import multivalued attribute not imported bug</span></span>
 * <span data-ttu-id="11860-182">Lors de l’exportation des valeurs supprimées\ajoutées d’un attribut à valeurs multiples, celles-ci ne sont pas supprimées\ajoutées dans la source de données.</span><span class="sxs-lookup"><span data-stu-id="11860-182">When exporting deleted\added values of multivalued attribute, they are not deleted\added in data source.</span></span>  


* <span data-ttu-id="11860-183">Lotus Notes :</span><span class="sxs-lookup"><span data-stu-id="11860-183">Lotus Notes:</span></span>
 * <span data-ttu-id="11860-184">Un champ « Nom complet » est indiqué dans le métaverse de hello correctement toutefois lors de l’exportation tooNotes hello valeur pour les attributs hello est Null ou vide.</span><span class="sxs-lookup"><span data-stu-id="11860-184">A specific field "Full Name" is shown in hello metaverse correctly however when exporting tooNotes hello value for hello attribute is Null or Empty.</span></span>
 * <span data-ttu-id="11860-185">Correction d’erreur de certification en double</span><span class="sxs-lookup"><span data-stu-id="11860-185">Fix for duplicate Certifier error</span></span>
 * <span data-ttu-id="11860-186">Lors de hello objet sans aucune donnée est sélectionnée sur hello connecteur pour Lotus Domino avec d’autres objets puis nous erreur hello découverte lors de l’importation complète.</span><span class="sxs-lookup"><span data-stu-id="11860-186">When hello Object without any data is selected on hello Lotus Domino Connector with other objects then we receive hello Discovery error while performing Full-Import.</span></span>
 * <span data-ttu-id="11860-187">Lors de l’importation de Delta est en cours d’exécution sur hello connecteur Lotus Domino à fin hello de cette exécution, hello Microsoft.IdentityManagement.MA.LotusDomino.Service.exe service parfois renvoie une erreur d’Application.</span><span class="sxs-lookup"><span data-stu-id="11860-187">When Delta Import is being running on hello Lotus Domino Connector, at hello end of that run, hello Microsoft.IdentityManagement.MA.LotusDomino.Service.exe service sometimes returns an Application Error.</span></span>
 * <span data-ttu-id="11860-188">L’appartenance au groupe global fonctionne correctement et est conservée, sauf lors de l’exécution hello exportation tootry tooremove un utilisateur d’appartenance, il montre aussi efficace avec une mise à jour, utilisateur de hello réellement ne sont supprimé de l’appartenance à Lotus Notes.</span><span class="sxs-lookup"><span data-stu-id="11860-188">Group membership overall works fine and is maintained, except when running hello export tootry tooremove a user from membership it shows as successful with an update, but hello user doesn’t actually get removed from membership in Lotus Notes.</span></span>
 * <span data-ttu-id="11860-189">Un mode de toochoose opportunité d’exportation en tant que « Ajouter l’élément bas » a été ajouté dans la configuration de l’interface graphique utilisateur de Lotus MA tooappend de nouveaux éléments en bas lors de l’exportation de hello pour les attributs à valeurs multiples.</span><span class="sxs-lookup"><span data-stu-id="11860-189">An opportunity toochoose mode of export as “Append Item at bottom” was added in configuration GUI of Lotus MA tooappend new items at bottom during hello export for multi-valued attributes.</span></span>
 * <span data-ttu-id="11860-190">Connecteur ajoutera hello nécessaire fichier hello logique toodelete hello dossier courrier et ID de coffre.</span><span class="sxs-lookup"><span data-stu-id="11860-190">Connector will add hello needed logic toodelete hello file from hello Mail Folder and ID Vault.</span></span>
 * <span data-ttu-id="11860-191">La suppression d’appartenance ne fonctionne pas pour un membre NAB croisé.</span><span class="sxs-lookup"><span data-stu-id="11860-191">Delete membership not working for cross NAB member.</span></span>
 * <span data-ttu-id="11860-192">Les valeurs devraient être supprimées correctement de l’attribut à valeurs multiples.</span><span class="sxs-lookup"><span data-stu-id="11860-192">Values should be successfully deleted from multi-valued attribute</span></span>

## <a name="111170"></a><span data-ttu-id="11860-193">1.1.117.0</span><span class="sxs-lookup"><span data-stu-id="11860-193">1.1.117.0</span></span>
<span data-ttu-id="11860-194">Publié : mars 2016</span><span class="sxs-lookup"><span data-stu-id="11860-194">Released: 2016 March</span></span>

<span data-ttu-id="11860-195">**Nouveau connecteur**</span><span class="sxs-lookup"><span data-stu-id="11860-195">**New Connector**</span></span>  
<span data-ttu-id="11860-196">Version de hello initiale [générique connecteur SQL](active-directory-aadconnectsync-connector-genericsql.md).</span><span class="sxs-lookup"><span data-stu-id="11860-196">Initial release of hello [Generic SQL Connector](active-directory-aadconnectsync-connector-genericsql.md).</span></span>

<span data-ttu-id="11860-197">**Nouvelles fonctionnalités :**</span><span class="sxs-lookup"><span data-stu-id="11860-197">**New features:**</span></span>

* <span data-ttu-id="11860-198">Connecteur LDAP générique :</span><span class="sxs-lookup"><span data-stu-id="11860-198">Generic LDAP Connector:</span></span>
  * <span data-ttu-id="11860-199">Prise en charge supplémentaire pour l’importation delta avec Isode.</span><span class="sxs-lookup"><span data-stu-id="11860-199">Added support for delta import with Isode.</span></span>
* <span data-ttu-id="11860-200">Connecteur des services web :</span><span class="sxs-lookup"><span data-stu-id="11860-200">Web Services Connector:</span></span>
  * <span data-ttu-id="11860-201">Hello mis à jour csEntryChangeResult activité et setImportErrorCode activité tooallow objet erreurs de niveau toobe toohello arrière retourné moteur de synchronisation.</span><span class="sxs-lookup"><span data-stu-id="11860-201">Updated hello csEntryChangeResult activity and setImportErrorCode activity tooallow object level errors toobe returned back toohello sync engine.</span></span>
  * <span data-ttu-id="11860-202">Hello mis à jour SAP6 et SAP6User modèles toouse hello nouvel objet erreur au niveau des fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="11860-202">Updated hello SAP6 and SAP6User templates toouse hello new object level error functionality.</span></span>
* <span data-ttu-id="11860-203">Connecteur Lotus Domino :</span><span class="sxs-lookup"><span data-stu-id="11860-203">Lotus Domino Connector:</span></span>
  * <span data-ttu-id="11860-204">Lors de l’exportation, vous avez besoin d’une autorité de certification par carnet d’adresses.</span><span class="sxs-lookup"><span data-stu-id="11860-204">For export, you need one certifier per address book.</span></span> <span data-ttu-id="11860-205">Vous pouvez maintenant utiliser hello même mot de passe pour toute certificateurs toomake hello la gestion plus facile.</span><span class="sxs-lookup"><span data-stu-id="11860-205">You can now use hello same password for all certifiers toomake hello management easier.</span></span>

<span data-ttu-id="11860-206">**Problèmes résolus :**</span><span class="sxs-lookup"><span data-stu-id="11860-206">**Fixed issues:**</span></span>

* <span data-ttu-id="11860-207">Connecteur LDAP générique :</span><span class="sxs-lookup"><span data-stu-id="11860-207">Generic LDAP Connector:</span></span>
  * <span data-ttu-id="11860-208">Pour IBM Tivoli DS, certains attributs de référence n’étaient pas été détectés correctement.</span><span class="sxs-lookup"><span data-stu-id="11860-208">For IBM Tivoli DS, some reference attributes were not detected correctly.</span></span>
  * <span data-ttu-id="11860-209">Pour LDAP ouvert pendant une importation delta, les espaces blancs au début de hello et la fin de chaînes a été tronqués.</span><span class="sxs-lookup"><span data-stu-id="11860-209">For Open LDAP during a delta import, whitespaces at hello beginning and end of strings were truncated.</span></span>
  * <span data-ttu-id="11860-210">Pour Novell et NetIQ, une exportation qui déplacer un objet entre les unités d’organisation/conteneurs et à hello même moment l’objet renommé hello a échoué.</span><span class="sxs-lookup"><span data-stu-id="11860-210">For Novell and NetIQ, an export that moved an object between OUs/containers and at hello same time renamed hello object failed.</span></span>
* <span data-ttu-id="11860-211">Connecteur des services web :</span><span class="sxs-lookup"><span data-stu-id="11860-211">Web Services Connector:</span></span>
  * <span data-ttu-id="11860-212">Si le service web de hello a plusieurs points de terminaison pour la même liaison, puis hello connecteur n’a pas correctement détecté ces points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="11860-212">If hello web service had multiple end-points for same binding, then hello Connector did not correctly discover these end-points.</span></span>
* <span data-ttu-id="11860-213">Connecteur Lotus Domino :</span><span class="sxs-lookup"><span data-stu-id="11860-213">Lotus Domino Connector:</span></span>
  * <span data-ttu-id="11860-214">Une exportation de hello fullName attribut tooa messagerie de base de données n’a pas fonctionné.</span><span class="sxs-lookup"><span data-stu-id="11860-214">An export of hello fullName attribute tooa mail-in database did not work.</span></span>
  * <span data-ttu-id="11860-215">Une exportation quel membre ajouté et supprimé à partir d’un groupe uniquement exportée hello membres ont été ajoutés.</span><span class="sxs-lookup"><span data-stu-id="11860-215">An export which both added and removed member from a group only exported hello added members.</span></span>
  * <span data-ttu-id="11860-216">Si un Document de notes de publication n’est pas valide (hello attribut isValid défini toofalse), puis hello échoue de connecteur.</span><span class="sxs-lookup"><span data-stu-id="11860-216">If a Notes Document is invalid (hello attribute isValid set toofalse), then hello Connector fails.</span></span>

## <a name="older-releases"></a><span data-ttu-id="11860-217">Versions plus anciennes</span><span class="sxs-lookup"><span data-stu-id="11860-217">Older releases</span></span>
<span data-ttu-id="11860-218">Avant mars 2016, hello connecteurs ont été publiés dans les rubriques de prise en charge.</span><span class="sxs-lookup"><span data-stu-id="11860-218">Before March 2016, hello Connectors were released as support topics.</span></span>

<span data-ttu-id="11860-219">**LDAP générique**</span><span class="sxs-lookup"><span data-stu-id="11860-219">**Generic LDAP**</span></span>

* <span data-ttu-id="11860-220">[KB3078617](https://support.microsoft.com/kb/3078617) - 1.0.0597, septembre 2015</span><span class="sxs-lookup"><span data-stu-id="11860-220">[KB3078617](https://support.microsoft.com/kb/3078617) - 1.0.0597, 2015 September</span></span>
* <span data-ttu-id="11860-221">[KB3044896](https://support.microsoft.com/kb/3044896) - 1.0.0549, mars 2015</span><span class="sxs-lookup"><span data-stu-id="11860-221">[KB3044896](https://support.microsoft.com/kb/3044896) - 1.0.0549, 2015 March</span></span>
* <span data-ttu-id="11860-222">[KB3031009](https://support.microsoft.com/kb/3031009) - 1.0.0534, janvier 2015</span><span class="sxs-lookup"><span data-stu-id="11860-222">[KB3031009](https://support.microsoft.com/kb/3031009) - 1.0.0534, 2015 January</span></span>
* <span data-ttu-id="11860-223">[KB3008177](https://support.microsoft.com/kb/3008177) - 1.0.0419, septembre 2014</span><span class="sxs-lookup"><span data-stu-id="11860-223">[KB3008177](https://support.microsoft.com/kb/3008177) - 1.0.0419, 2014 September</span></span>
* <span data-ttu-id="11860-224">[KB2936070](https://support.microsoft.com/kb/2936070) - 4.3.1082, mars 2014</span><span class="sxs-lookup"><span data-stu-id="11860-224">[KB2936070](https://support.microsoft.com/kb/2936070) - 4.3.1082, 2014 March</span></span>

<span data-ttu-id="11860-225">**WebServices**</span><span class="sxs-lookup"><span data-stu-id="11860-225">**WebServices**</span></span>

* <span data-ttu-id="11860-226">[KB3008178](https://support.microsoft.com/kb/3008178) - 1.0.0419, septembre 2014</span><span class="sxs-lookup"><span data-stu-id="11860-226">[KB3008178](https://support.microsoft.com/kb/3008178) - 1.0.0419, 2014 September</span></span>

<span data-ttu-id="11860-227">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="11860-227">**PowerShell**</span></span>

* <span data-ttu-id="11860-228">[KB3008179](https://support.microsoft.com/kb/3008179) - 1.0.0419, septembre 2014</span><span class="sxs-lookup"><span data-stu-id="11860-228">[KB3008179](https://support.microsoft.com/kb/3008179) - 1.0.0419, 2014 September</span></span>

<span data-ttu-id="11860-229">**Lotus Domino**</span><span class="sxs-lookup"><span data-stu-id="11860-229">**Lotus Domino**</span></span>

* <span data-ttu-id="11860-230">[KB3096533](https://support.microsoft.com/kb/3096533) - 1.0.0597, septembre 2015</span><span class="sxs-lookup"><span data-stu-id="11860-230">[KB3096533](https://support.microsoft.com/kb/3096533) - 1.0.0597, 2015 September</span></span>
* <span data-ttu-id="11860-231">[KB3044895](https://support.microsoft.com/kb/3044895) - 1.0.0549, mars 2015</span><span class="sxs-lookup"><span data-stu-id="11860-231">[KB3044895](https://support.microsoft.com/kb/3044895) - 1.0.0549, 2015 March</span></span>
* <span data-ttu-id="11860-232">[KB2977286](https://support.microsoft.com/kb/2977286) - 5.3.0712, août 2014</span><span class="sxs-lookup"><span data-stu-id="11860-232">[KB2977286](https://support.microsoft.com/kb/2977286) - 5.3.0712, 2014 August</span></span>
* <span data-ttu-id="11860-233">[KB2932635](https://support.microsoft.com/kb/2932635) - 5.3.1003, février 2014</span><span class="sxs-lookup"><span data-stu-id="11860-233">[KB2932635](https://support.microsoft.com/kb/2932635) - 5.3.1003, 2014 February</span></span>  
* <span data-ttu-id="11860-234">[KB2899874](https://support.microsoft.com/kb/2899874) - 5.3.0721, octobre 2013</span><span class="sxs-lookup"><span data-stu-id="11860-234">[KB2899874](https://support.microsoft.com/kb/2899874) - 5.3.0721, 2013 October</span></span>
* <span data-ttu-id="11860-235">[KB2875551](https://support.microsoft.com/kb/2875551) - 5.3.0534, août 2013</span><span class="sxs-lookup"><span data-stu-id="11860-235">[KB2875551](https://support.microsoft.com/kb/2875551) - 5.3.0534, 2013 August</span></span>

## <a name="next-steps"></a><span data-ttu-id="11860-236">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="11860-236">Next steps</span></span>
<span data-ttu-id="11860-237">En savoir plus sur hello [synchronisation Azure AD Connect](active-directory-aadconnectsync-whatis.md) configuration.</span><span class="sxs-lookup"><span data-stu-id="11860-237">Learn more about hello [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="11860-238">En savoir plus sur l’ [intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="11860-238">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
