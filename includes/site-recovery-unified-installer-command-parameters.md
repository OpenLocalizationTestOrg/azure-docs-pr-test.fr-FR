|Nom du paramètre| Type | Description| Valeurs possibles|
|-|-|-|-|
| /ServerMode|Obligatoire|Spécifie si les deux serveurs de configuration et les processus hello doivent être installés ou le serveur de processus hello uniquement|CS<br>PS|
|/InstallLocation|Obligatoire|dossier Hello dans le hello composants sont installés| N’importe quel dossier sur l’ordinateur de hello|
|/MySQLCredsFilePath|Obligatoire|chemin d’accès du fichier Hello dans le hello MySQL server sont stockées|fichier de Hello doit être au format hello spécifié ci-dessous|
|/VaultCredsFilePath|Obligatoire|chemin d’accès de Hello du fichier d’informations d’identification de coffre hello|Chemin d’accès valide du fichier|
|/EnvType|Obligatoire|Type d’environnement que vous souhaitez tooprotect |VMware<br>NonVMware|
|/PSIP|Obligatoire|Adresse IP de hello toobe de carte réseau utilisée pour le transfert de données de réplication| Une adresse IP valide|
|/CSIP|Obligatoire|adresse IP de Hello de NIC hello sur quel hello écoute sur serveur de configuration| Une adresse IP valide|
|/PassphraseFilePath|Obligatoire|Hello toolocation de chemin d’accès complet du fichier de mot de passe hello|Chemin d’accès valide du fichier|
|/BypassProxy|Facultatif|Ce serveur de configuration hello se connecte tooAzure sans proxy|toodo obtenir cette valeur à partir de Venu|
|/ProxySettingsFilePath|Facultatif|Paramètres de proxy (proxy par défaut de hello requiert l’authentification ou un proxy personnalisé)|fichier de Hello doit être au format hello spécifiée ci-dessous|
|DataTransferSecurePort|Facultatif|Numéro de port sur hello PSIP toobe est utilisé pour les données de réplication| Numéro de port valide (valeur par défaut : 9433)|
|/SkipSpaceCheck|Facultatif|Ignorer la vérification des espaces pour le disque du cache| |
|/AcceptThirdpartyEULA|Obligatoire|Cet indicateur implique l’acceptation du CLUF tiers| |
|/ShowThirdpartyEULA|Facultatif|Affiche le CLUF tiers. S’il est fourni en entrée, tous les autres paramètres sont ignorés| |
