**LAB 2 : Rooting Android**
Étape 1 : Rooter l'AVD

<img width="830" height="151" alt="image" src="https://github.com/user-attachments/assets/be148751-ef65-4154-bc9b-2e5cedeb484c" />

>Cette capture d'écran illustre l'étape initiale de l'interaction avec un appareil Android via le Android Debug Bridge (ADB). C'est une phase cruciale pour tout audit de sécurité ou test d'intrusion mobile.
>Utilisation de la commande adb devices pour lister les terminaux connectés. On observe qu'un émulateur Android (emulator-5554) est correctement détecté et prêt à recevoir des instructions via le pont de débogage Android (ADB).
<img width="911" height="251" alt="image" src="https://github.com/user-attachments/assets/75c74a4b-916f-44f8-afab-331afaf2b3f9" />

>Exécution de la commande adb root. Le système confirme le redémarrage du démon ADB (adbd) avec les droits d'administrateur (root). Cette étape est cruciale pour accéder aux fichiers système sensibles et effectuer des tests d'intrusion sur l'application mobile.




<img width="1800" height="748" alt="image" src="https://github.com/user-attachments/assets/ce564363-4629-4fca-8a54-57c905bba480" />


1. ```adb root```
Description : Redémarre le démon ADB (adbd) sur l'appareil avec les privilèges root (administrateur). Cela permet d'accéder aux fichiers système protégés.

2. ```adb shell id```
Description : Affiche l'identité de l'utilisateur actuel dans le shell Android. Dans votre cas, il confirme que vous êtes uid=0(root), ce qui signifie que vous avez les pleins pouvoirs sur le système.

3. ```adb shell getprop ro.boot.verifiedbootstate```
Description : Interroge la propriété système pour vérifier l'état du Verified Boot. Cela permet de savoir si le chargeur de démarrage (bootloader) est verrouillé ou si l'intégrité du système est compromise.

4. ```adb shell getprop ro.boot.veritymode```
Description : Vérifie le mode de dm-verity. Dans votre capture, il répond enforcing, ce qui signifie que le système vérifie strictement l'intégrité des partitions au démarrage et empêche les modifications non autorisées.

5. ```adb shell getprop ro.boot.vbmeta.device_state```
Description : Indique l'état actuel de la sécurité de l'appareil (généralement locked ou unlocked) basé sur les métadonnées de démarrage sécurisé (vbmeta).

6. ```adb shell "su -c id"```
Description : Tente d'exécuter la commande id en passant par l'utilitaire su (SuperUser).

Note sur l'erreur : Elle a échoué (invalid uid/gid '-c') parce que sur certains émulateurs ou versions d'Android, la syntaxe du binaire su est différente ou le paramètre -c n'est pas reconnu de cette manière. Cependant, comme vous êtes déjà en mode adb root, cette commande est redondante.

<img width="1248" height="264" alt="image" src="https://github.com/user-attachments/assets/2af064f2-93a2-488c-91bb-a59ed9e68939" />
# Journalisation :
<img width="1401" height="117" alt="image" src="https://github.com/user-attachments/assets/65296c20-4532-4b32-8f16-10292a831dd7" />
cette commande nessaicite une aparaile physique
<img width="943" height="102" alt="image" src="https://github.com/user-attachments/assets/07b1262a-3669-49d4-8f7e-0085b436db8b" />
# Resultat de fichier de log 
<img width="1239" height="999" alt="image" src="https://github.com/user-attachments/assets/5a958631-eeba-46d7-8662-1d27b6e08e27" />

## 📋 Étape 2 : Fiche Périmètre de l'Audit de Sécurité

Cette section définit le cadre technique et les limites de l'audit de sécurité réalisé sur l'application mobile.

| Élément | Détails de l'Audit |
| :--- | :--- |
| **Application & Version** | `DIVA` (v1.0) |
| **Support de Test** | Émulateur Android (AVD) sur HP EliteBook 830 G5 |
| **Système d'Exploitation** | Android (Rooté via ADB) |
| **Objectif Principal** | Analyse du processus de root et évaluation des vulnérabilités système |
| **Données de Test** | Données fictives uniquement (Aucune donnée réelle) |
| **Environnement Réseau** | Réseau local isolé (Lab Environment) |
| **Outils Utilisés** | ADB (Android Debug Bridge), PowerShell |

### 🛡️ Justification du Périmètre
Le périmètre a été défini pour garantir un environnement de test **maîtrisé** et **éthique**. L'utilisation de données fictives et d'un réseau isolé permet d'éviter tout impact sur des systèmes de production ou des données personnelles réelles.
# Étape 3 : Démarrer un AVD propre
<img width="830" height="151" alt="image" src="https://github.com/user-attachments/assets/be148751-ef65-4154-bc9b-2e5cedeb484c" />

# Étape 4 : Installer et lancer l'app de test
<img width="1733" height="984" alt="image" src="https://github.com/user-attachments/assets/5c784f26-08f9-4d48-8cb1-28d9f1cec291" />

# Étape 5 : Définir 3 scénarios simples
* Ouvrir l'écran d'accueil

<img width="575" height="1033" alt="image" src="https://github.com/user-attachments/assets/6c5fa84e-5f95-4b34-9a3f-52a7c2a35ccf" />
* Ouvrir un détail (fiche produit/profil)
<img width="452" height="932" alt="image" src="https://github.com/user-attachments/assets/d9d04054-bda0-42d8-b20b-79eff5717e8c" />

* Rechercher un item
<img width="450" height="824" alt="image" src="https://github.com/user-attachments/assets/2a26a641-d9f2-456f-aac2-a21df168175b" />
* Ouvrir un détail (fiche produit/profil)

  # Étape 6 : Lire Android Security (6 lignes max)
  Lien : https://source.android.com/docs/security
  <img width="1316" height="742" alt="image" src="https://github.com/user-attachments/assets/a69132d1-d634-47f9-94af-435e64f615e4" />
  * resume :

La sécurité Android repose sur une structure multi-couches protégeant les données et le système. Le sandboxing isole chaque application dans un environnement fermé pour empêcher l'accès aux données des autres apps. Le modèle de permissions assure un contrôle strict sur l'accès aux ressources sensibles comme les contacts ou la caméra. Enfin, l'isolation et l'intégrité globale verrouillent le système contre les modifications non autorisées. Le rooting compromet ces barrières en offrant un accès total, ce qui brise la structure de protection native. Ce mécanisme est comparable à un bâtiment sécurisé dont on forcerait les portes blindées.
# Étape 7 : Analyse du Verified Boot (Démarrage Vérifié)
* 1. Concepts Fondamentaux :
    *  Objectif principal : Garantir que le système d'exploitation qui démarre est exactement celui prévu par le fabricant, sans aucune modification malveillante.

* Chain of Trust (Chaîne de confiance) :
   C'est une série de vérifications où chaque composant matériel ou logiciel vérifie l'authenticité du suivant avant de lui accorder sa confiance, comme une suite de gardiens vérifiant l'identité du suivant.

* Importance de l'intégrité : Si le démarrage est compromis, toutes les protections de sécurité ultérieures peuvent être contournées, comme une forteresse dont la porte principale resterait ouverte.
    <br> ``` adb shell getprop ro.boot.verifiedbootstate ```
<img width="960" height="93" alt="image" src="https://github.com/user-attachments/assets/a634409d-2c85-42bc-8a6a-0ee80cf4bc58" />

# Résumé de la technologie (3 lignes) :
L'AVB introduit une vérification d'intégrité moderne qui assure que chaque partition du système est authentique avant d'être chargée. Il ajoute également une protection contre le rollback, empêchant l'installation de versions obsolètes du système qui pourraient contenir des failles de sécurité connues. Ce mécanisme garantit que l'appareil reste toujours sur une version logicielle sécurisée et approuvée.


# Résumé en 4 phrases :
Le rooting consiste à acquérir les privilèges de "super-utilisateur" sur le système Android, permettant de dépasser les restrictions imposées par le fabricant. Cette action modifie profondément les mécanismes de protection natifs et la confiance globale du système d'exploitation. Bien qu'utile en laboratoire pour observer des comportements techniques précis, cette manipulation reste risquée car elle expose l'appareil à des menaces accrues. Par conséquent, un environnement rooté nécessite un isolement strict, une traçabilité complète des actions et un reset systématique après les tests.
# Étape 10 : Intérêt labo (non opérationnel)

Dans un cadre de laboratoire, un environnement privilégié peut aider à plusieurs niveaux pour sécuriser une application comme GestionDesTaches3 :

- **Observation des artefacts système** : Accéder à des fichiers et répertoires normalement invisibles pour un utilisateur standard.

- **Analyse bas niveau** : Examiner en temps réel comment l'application se comporte et interagit avec le noyau du système.

- **Test de robustesse** : Vérifier si le stockage des données résiste à un attaquant possédant déjà les droits d'administrateur.

- **Cas d'usage concret** : Avec les privilèges root, nous pouvons vérifier si l'application stocke ses données sensibles en clair en se reposant uniquement sur la protection du système (mauvaise pratique) ou si elle implémente son propre chiffrement (bonne pratique).
- 

##  Étape 11 : Matrice de Risques de l'Audit

| Risque Identifié | Impact sur l'Audit | Mesure d'Atténuation |
| :--- | :--- | :--- |
| **Intégrité compromise** | Conclusions biaisées | Utilisation d'images système certifiées |
| **Fuite de données** | Violation de confidentialité | Utilisation stricte de données fictives |
| **Instabilité** | Résultats incohérents | Snapshots et resets fréquents de l'AVD |
| **Persistance** | Fuite d'infos post-test | Nettoyage complet après chaque session |
| **Effets réseau** | Impact sur tiers | Isolation via réseau de test dédié |

> **Principe de sécurité :** Chaque risque identifié est associé à une mesure d'atténuation pour garantir la fiabilité de la gestion des risques en cybersécurité.
> 
## 🛡️ Gestion des Risques et Mesures Défensives

L'audit de sécurité sur un environnement rooté nécessite des protocoles stricts, comparables à la manipulation de substances dangereuses en laboratoire.

###  Matrice des Risques (Étape 11)
- **Intégrité** : Risque de conclusions biaisées sur la sécurité réelle.
- **Confidentialité** : Fuite possible si des données réelles sont présentes.
- **Traçabilité** : Risque d'incapacité à reproduire les tests sans logs précis.

###  Mesures de Protection Appliquées (Étape 12)
| Mesure | Objectif de Sécurité |
| :--- | :--- |
| **Isolation Réseau** | Éviter les communications non contrôlées. |
| **Données Fictives** | Zéro risque de fuite réelle. |
| **Wipe & Snapshot** | Décontamination de l'environnement post-test. |
| **Zéro Compte Perso** | Étanchéité totale entre vie privée et labo. |

> **Conclusion de l'Audit** : Les vérifications (`adb shell id` -> `uid=0`) ont confirmé que l'environnement est prêt pour l'analyse en profondeur de l'application **GestionDesTaches3** dans un cadre sécurisé et maîtrisé.
> ##  Conformité et Standards (OWASP MASVS)

L'utilisation des privilèges root (`uid=0`) a permis de confronter l'application aux standards industriels de sécurité mobile.

| Exigence OWASP | Description | Application Pratique |
| :--- | :--- | :--- |
| **STORAGE-1** | Chiffrement des données sensibles au repos. | Vérification des fichiers de stockage local via le shell root. |
| **NETWORK-1** | Utilisation sécurisée de TLS pour le réseau. | Interception du trafic pour valider la vérification des certificats. |

###  Conclusion de l'Audit
Ce laboratoire a permis de démontrer l'importance de la chaîne de confiance (Chain of Trust) et les risques liés à l'élévation de privilèges. Bien que le rooting compromette l'intégrité globale (`verifiedbootstate` passif), il est un outil d'analyse indispensable pour valider la robustesse d'une application face à des attaquants sophistiqués

##  Méthodologie de Test Pratique (OWASP MASTG)

Le passage au mode root a permis d'appliquer le guide de test **MASTG** pour une inspection approfondie de l'application.

| Scénario de Test | Outils & Commandes | Objectif de Sécurité |
| :--- | :--- | :--- |
| **Inspection Filesystem** | `cd /data/data/` | Détecter le stockage de données sensibles en clair. |
| **Analyse Runtime** | `adb logcat` | Identifier les fuites d'informations dans les logs. |

###  Conclusion Générale du Labo
Cet audit a couvert l'intégralité de la chaîne de sécurité :
1. **Périmètre** : Définition claire des limites de l'audit.
2. **Intégrité** : Analyse du Verified Boot et de la Chain of Trust.
3. **Escalade** : Validation de l'accès root pour l'analyse bas niveau.
4. **Conformité** : Vérification face aux standards OWASP MASVS/MASTG.
5. **Éthique** : Application de mesures défensives strictes pour protéger l'environnement de test.












