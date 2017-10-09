1. Copiez hello installer tooa dossier local (par exemple, /tmp) sur le serveur hello que tooprotect. Dans un terminal, exécutez hello suivant de commandes :
  ```
  cd /tmp
  tar -xvzf Microsoft-ASR_UA*release.tar.gz
  ```
2. tooinstall Service mobilité, exécutez hello de commande suivante :

  ```
  sudo ./install -d <Install Location> -r MS -v VmWare -q
  ```
3. Une fois l’installation terminée, hello Service mobilité a besoin de serveur de configuration tooget toohello inscrits. Exécutez hello suivant commande tooregister hello Service mobilité avec le serveur de Configuration.

  ```
  /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <CSIP> -P /var/passphrase.txt
  ```

#### <a name="mobility-service-installer-command-line"></a>Ligne de commande du programme d’installation du service Mobilité

```
Usage:
./install -d <Install Location> -r <MS|MT> -v VmWare -q
```

|Paramètre|Type|Description|Valeurs possibles|
|-|-|-|-|
|-r |Obligatoire|Spécifie si le service Mobilité (MS) doit être installé ou si MasterTarget(MT) doit être installé|MS </br> MT|
|-d |Facultatif|Emplacement où sera installé le service Mobilité|/usr/local/ASR|
|-v|Obligatoire|Spécifie la plateforme hello sur quel hello Service mobilité est installé </br> </br>- **VMware** : utilisez cette valeur si vous installez le service Mobilité sur une machine virtuelle exécutée sur des *hôtes VMware vSphere ESXi*, des *hôtes Hyper-V* et des *serveurs physiques* </br> - **Azure** : utilisez cette valeur si vous installez l’agent sur une machine virtuelle Azure IaaS| VMware </br> Les tables Azure|
|-q|Facultatif|Spécifie le programme d’installation toorun en mode silencieux| N/A|


#### <a name="mobility-service-configuration-command-line"></a>Ligne de commande de configuration du service Mobilité

```
Usage:
cd /usr/local/ASR/Vx/bin
UnifiedAgentConfigurator.sh -i <CSIP> -P <PassphraseFilePath>
```

|Paramètre|Type|Description|Valeurs possibles|
|-|-|-|-|
|-i |Obligatoire|Adresse IP du serveur de Configuration de hello|Une adresse IP valide|
|-P |Obligatoire|Fichier de hello de chemin d’accès complet du fichier où le mot de passe de connexion hello est enregistré|N’importe quel dossier valide|
