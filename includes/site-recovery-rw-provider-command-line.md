UnifiedSetup.exe [/ ServerMode < CS/PS >] [/ Lecteurinstall <DriveLetter>] [/ MySQLCredsFilePath <MySQL credentials file path>] [/ VaultCredsFilePath <Vault credentials file path>] [/ EnvType < VMWare/NonVMWare >] [/ PSIP < toobe d’adresse IP utilisée pour le transfert de données] [/CSIP <IP address of CS toobe registered with>] [/ PassphraseFilePath <Passphrase file path>]

Paramètres :

* /ServerMode : Obligatoire. Spécifie si les deux serveurs de configuration et les processus hello doivent être installés ou le serveur de processus hello uniquement. Valeurs d’entrée : CS, PS.
* InstallLocation : Obligatoire. dossier Hello dans le hello composants sont installés.
* /MySQLCredsFilePath. Obligatoire. chemin de fichier Hello dans le hello MySQL server sont stockées. fichier de Hello doit être au format suivant :
* [MySQLCredentials]
* MySQLRootPassword = "<Password>"
* MySQLUserPassword = "<Password>"
* /VaultCredsFilePath. Obligatoire. emplacement de Hello du fichier d’informations d’identification de coffre hello
* / EnvType. Obligatoire. type Hello d’installation. Valeurs : VMware, NonVMware
* / PSIP et /CSIP. Obligatoire. adresse IP de Hello du serveur de processus hello et serveur de configuration.
* /PassphraseFilePath. Obligatoire. emplacement de Hello du fichier de mot de passe de hello.
* /BypassProxy. facultatif. Spécifie que ce serveur de configuration hello connecte tooAzure sans proxy.
* /ProxySettingsFilePath. facultatif. Paramètres de proxy (proxy par défaut de hello requiert l’authentification ou un proxy personnalisé). fichier de Hello doit être au format suivant :
* [ProxySettings]
* ProxyAuthentication = "Oui/Non"
* Proxy IP = "Adresse IP>"
* ProxyPort = "<Port>"
* ProxyUserName="<User Name>"
* ProxyPassword="<Password>"
* DataTransferSecurePort. facultatif. numéro de port Hello pour les données de réplication.
* SkipSpaceCheck. facultatif. Vérification de l’omission des espaces pour le cache.
* AcceptThirdpartyEULA. Obligatoire. Accepte le CLUF de tiers hello.
* ShowThirdpartyEULA. Obligatoire. Affiche le CLUF tiers. S’il est fourni en tant qu’entrée, tous les autres paramètres sont ignorés.
