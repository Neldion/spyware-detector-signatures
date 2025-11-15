# Base de données de signatures de spyware

Ce fichier JSON contient les signatures de spyware, stalkerware et applications de surveillance utilisées par l'application Détecteur de Spyware.

## Structure du fichier `signatures.json`

```json
{
  "version": 1,                    // Numéro de version (incrémenté à chaque mise à jour)
  "last_updated": "2025-11-15",    // Date de dernière mise à jour
  "spyware_packages": [...],       // Liste des packages de spyware connus
  "parental_control_packages": [...], // Applications de contrôle parental
  "suspicious_keywords": [...]     // Mots-clés suspects dans les noms de packages
}
```

### Format d'une signature de spyware

```json
{
  "package_name": "com.example.spyware",
  "name": "Nom du spyware",
  "category": "commercial_spyware",
  "severity": 100,
  "description": "Description détaillée",
  "source": "coalition"
}
```

### Catégories disponibles

- `commercial_spyware`: Logiciels espions commerciaux
- `stalkerware`: Applications de surveillance malveillantes
- `parental_control`: Applications de contrôle parental (légitimes mais invasives)
- `surveillance`: Applications de surveillance générale
- `tracker`: Trackers publicitaires invasifs

### Niveaux de sévérité

- `100`: Critique - Spyware commercial confirmé, très invasif
- `90-99`: Très élevé - Spyware très suspect
- `70-89`: Élevé - Application de surveillance invasive
- `50-69`: Moyen - Contrôle parental ou surveillance modérée
- `1-49`: Faible - Tracker ou application légèrement suspecte

### Sources

- `coalition`: Coalition Against Stalkerware
- `exodus`: Exodus Privacy
- `manual`: Ajout manuel vérifié
- `github`: Contribution communautaire

## Comment mettre à jour les signatures

### Option 1: Hébergement sur GitHub (recommandé)

1. Créez un repository public GitHub nommé `spyware-detector-signatures`
2. Uploadez le fichier `signatures.json` à la racine
3. L'application téléchargera automatiquement les mises à jour une fois par jour
4. URL utilisée: `https://raw.githubusercontent.com/fperthuis/spyware-detector-signatures/main/signatures.json`

### Option 2: Fork et Pull Request

1. Forkez le repository
2. Modifiez le fichier `signatures.json`
3. Incrémentez le numéro de `version`
4. Mettez à jour `last_updated` avec la date actuelle
5. Créez une Pull Request

### Option 3: Mise à jour locale

Pour tester en local avant de publier:

1. Modifiez le fichier `signatures.json`
2. Incrémentez la version
3. Hébergez temporairement sur un serveur web
4. Modifiez l'URL dans `NetworkModule.kt` (baseUrl du retrofit "signatures")

## Sources de données recommandées

### 1. Coalition Against Stalkerware
- Website: https://stopstalkerware.org
- Liste des membres et ressources sur les stalkerware

### 2. Exodus Privacy
- Website: https://exodus-privacy.eu.org
- API: https://reports.exodus-privacy.eu.org/api/
- Trackers invasifs dans les applications Android

### 3. TinyCheck (Kaspersky)
- GitHub: https://github.com/KasperskyLab/tinycheck
- IoC (Indicators of Compromise) pour stalkerware

### 4. SpyGuard
- GitHub: https://github.com/SpyGuard/SpyGuard
- Fork amélioré de TinyCheck

### 5. Android Stalkerware Research
- GitHub: https://github.com/diskurse/android-stalkerware
- Analyses communautaires de stalkerware

## Contribuer

Pour ajouter un nouveau spyware:

1. Vérifiez qu'il n'existe pas déjà dans la liste
2. Collectez les informations nécessaires:
   - Package name exact
   - Nom commercial
   - Catégorie appropriée
   - Niveau de sévérité justifié
   - Description des capacités
   - Source de l'information
3. Ajoutez l'entrée dans `spyware_packages`
4. Incrémentez le numéro de version
5. Créez une Pull Request avec vos sources

## Fréquence de mise à jour recommandée

- **Version initiale**: 1 (contenu actuel)
- **Mises à jour mineures**: Ajout de nouveaux spyware (incrément de 1)
- **Mises à jour majeures**: Refonte de la structure (incrément de 10+)

## Notes importantes

⚠️ **Attention**: Cette base de données ne peut pas détecter tous les spywares. L'application utilise également:
- Détection heuristique (permissions dangereuses, combinaisons suspectes)
- API Exodus Privacy en temps réel
- Liste blanche de packages système légitimes Android

⚠️ **Faux positifs**: Les applications de contrôle parental légitimes sont incluses car elles peuvent être utilisées de manière abusive. L'utilisateur doit décider si leur présence est légitime.

## Licence

Cette base de données est fournie sous licence Open Database License (ODbL).
Les contributions sont les bienvenues et doivent être vérifiées et sourcées.

## Contact

Pour signaler un spyware ou proposer des améliorations:
- Créez une issue sur GitHub
- Proposez une Pull Request avec vos sources
