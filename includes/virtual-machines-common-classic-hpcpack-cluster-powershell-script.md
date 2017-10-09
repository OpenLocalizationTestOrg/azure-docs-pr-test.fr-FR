



Selon votre environnement et le choix, script de hello peut créer toute infrastructure de cluster hello, y compris hello réseau virtuel Azure, comptes de stockage, services de cloud computing, contrôleur de domaine, les bases de données SQL locales ou distantes, nœud principal et cluster supplémentaires nœuds. Vous pouvez également script de hello peut utiliser l’infrastructure Azure existante et créer uniquement les nœuds de cluster HPC hello.

Pour des informations générales sur la planification d’un cluster HPC Pack, consultez hello [d’évaluation du produit et planification](https://technet.microsoft.com/library/jj899596.aspx) et [mise en route](https://technet.microsoft.com/library/jj899590.aspx) contenu Bonjour bibliothèque TechNet de HPC Pack 2012 R2.

## <a name="prerequisites"></a>Composants requis
* **Abonnement Azure**: vous pouvez utiliser un abonnement soit Bonjour service Global Azure ou Azure Chine. Limites de votre abonnement affectent hello nombre et type que vous pouvez déployer des nœuds de cluster. Pour plus d’informations, consultez [Abonnement Azure et limites, quotas et contraintes du service](../articles/azure-subscription-service-limits.md).
* **Ordinateur client Windows Azure PowerShell 0.8.10 ou version ultérieure installé et configuré**: consultez [prise en main Azure PowerShell](/powershell/azureps-cmdlets-docs) pour tooconnect de procédures et instructions installation tooyour abonnement Azure.
* **Script de déploiement IaaS de HPC Pack**: Téléchargez et décompressez hello dernière version de script hello hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949). Vérifier la version de hello du script de hello en exécutant `New-HPCIaaSCluster.ps1 –Version`. Cet article est basé sur la version 4.5.2 du script de hello.
* **Fichier de configuration**: créer un fichier XML que le script de hello utilise cluster HPC de hello tooconfigure. Pour plus d’informations et des exemples, consultez les sections plus loin dans cet article et hello fichier Manual.rtf qui accompagne le script de déploiement hello.

## <a name="syntax"></a>Syntaxe
```PowerShell
New-HPCIaaSCluster.ps1 [-ConfigFile] <String> [-AdminUserName]<String> [[-AdminPassword] <String>] [[-HPCImageName] <String>] [[-LogFile] <String>] [-Force] [-NoCleanOnFailure] [-PSSessionSkipCACheck] [<CommonParameters>]
```
> [!NOTE]
> Exécutez le script de hello en tant qu’administrateur.
> 
> 

### <a name="parameters"></a>Paramètres
* **ConfigFile**: Spécifie le chemin d’accès du fichier hello hello configuration toodescribe hello HPC du cluster de fichiers. Voir plus d’informations sur le fichier de configuration hello dans cette rubrique, ou dans le fichier de hello Manual.rtf dans le dossier hello contenant un script de hello.
* **AdminUserName**: Spécifie le nom d’utilisateur hello. Si la forêt de domaines hello est créée par le script de hello, cela devient le nom d’utilisateur administrateur local hello pour toutes les machines virtuelles et le nom d’administrateur de domaine de hello. Si la forêt de domaines hello existe déjà, cela spécifie l’utilisateur de domaine hello comme hello tooinstall de nom d’utilisateur administrateur local HPC Pack.
* **AdminPassword**: Spécifie le mot de passe d’administrateur hello. Si non spécifié dans la ligne de commande hello, script de hello vous invite mot de passe tooinput hello.
* **HPCImageName** (facultatif) : Spécifie le nom d’image de machine virtuelle HPC Pack de hello utilisé cluster HPC de hello toodeploy. Il doit être une image fournie par Microsoft HPC Pack à partir de hello Azure Marketplace. Si non spécifié hello (recommandé en général), script choisit la dernière version publiée de hello [image HPC Pack 2012 R2](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/). image plus récente de Hello est basée sur Windows Server 2012 R2 Datacenter avec HPC Pack 2012 R2 Update 3.
  
  > [!NOTE]
  > Le déploiement échoue si vous ne spécifiez pas d’image HPC Pack valide.
  > 
  > 
* **Fichier journal** (facultatif) : Spécifie le chemin d’accès du journal de déploiement hello. Si non spécifié, le script de hello crée un fichier journal dans le répertoire temp de l’ordinateur hello exécutant hello script hello.
* **Force** (facultatif) : supprime toutes les invites de confirmation hello.
* **NoCleanOnFailure** (facultatif) : Spécifie que hello machines virtuelles Azure qui ne sont pas déployés avec succès ne sont pas supprimés. Supprimez ces machines virtuelles manuellement avant de réexécuter le déploiement hello script toocontinue hello ou hello déploiement peut échouer.
* **PSSessionSkipCACheck** (facultatif) : pour chaque service cloud avec des machines virtuelles déployées par ce script, un certificat auto-signé est généré automatiquement par Azure et hello toutes les machines virtuelles dans le service cloud hello utiliser ce certificat comme hello Windows par défaut Certificat de gestion (WinRM) à distance. toodeploy les fonctionnalités HPC dans ces machines virtuelles Azure, script hello par défaut installe temporairement ces certificats Bonjour ordinateur Local\\magasin Autorités de Certification racine de hello client ordinateur toosuppress hello « autorité de certification non approuvée » de sécurité Erreur lors de l’exécution du script. certificats de Hello sont supprimés lorsque hello script se termine. Si ce paramètre est spécifié, les certificats hello ne sont pas installés dans l’ordinateur client de hello et avertissement de sécurité hello est supprimé.
  
  > [!IMPORTANT]
  > Ce paramètre n’est pas recommandé pour les déploiements de production.
  > 
  > 

### <a name="example"></a>Exemple
Hello exemple suivant crée un cluster HPC Pack à l’aide du fichier de configuration *MyConfigFile.xml*et spécifie les informations d’identification d’administrateur pour l’installation de cluster de hello.

```PowerShell
.\New-HPCIaaSCluster.ps1 –ConfigFile MyConfigFile.xml -AdminUserName <username> –AdminPassword <password>
```

### <a name="additional-considerations"></a>Considérations supplémentaires
* script de Hello peut également activer la soumission de travaux via le portail web de HPC Pack hello ou hello API REST de HPC Pack.
* script de Hello peut également exécuter des scripts de pré- et post-configuration personnalisés sur le nœud principal de hello si vous souhaitez tooinstall des logiciels supplémentaires ou configurez d’autres paramètres.

## <a name="configuration-file"></a>Fichier de configuration
le fichier de configuration Hello pour le script de déploiement hello est un fichier XML. fichier de schéma Hello HPCIaaSClusterConfig.xsd se trouve dans le dossier de scripts de déploiement IaaS de HPC Pack hello. **IaaSClusterConfig** est l’élément racine de hello hello du fichier de configuration, qui contienne des éléments enfants hello décrits en détail dans le fichier hello Manual.rtf dans le dossier des scripts de déploiement hello.

