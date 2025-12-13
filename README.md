# 🎬 LTC sur Bande Magnétique - Visualisation Interactive

Une visualisation pédagogique interactive démontrant le comportement du **Linear Time Code (LTC)** sur bande magnétique lors de la lecture à vitesse variable.

🔗 **[Voir la démonstration en ligne](https://plhfak.github.io/ltc-visualisation/)**

---

## 📖 Description

Ce projet illustre de manière visuelle et technique comment le **LTC (Linear Time Code)** se comporte lorsqu'il est enregistré sur une bande magnétique puis lu à une vitesse différente. 

### Démonstration

La visualisation compare deux scénarios :

1. **⏺ RECORD (100%)** : Signal LTC généré et enregistré à vitesse normale (50 fps)
2. **▶️ PLAYBACK RALENTI (33%)** : Même signal lu à 33% de la vitesse originale

**Résultat clé** : Le timecode reste **parfaitement décodable** malgré le changement de vitesse, grâce à l'encodage biphase auto-synchronisant du LTC.

---

## 🎯 Cas d'Usage

### Pédagogie
- Formation des techniciens broadcast
- Cours sur la synchronisation vidéo professionnelle
- Démonstration du principe de timecode SMPTE

### Professionnel
- Documentation technique pour équipes de post-production
- Support de présentation pour clients
- Référence pour développeurs de systèmes de timecode

### Technique
- Compréhension du shuttle/jog sur magnétoscopes
- Analyse des effets de vitesse variable sur le LTC
- Étude de la robustesse du timecode

---

## 📊 Spécifications Techniques

### Signal LTC (RECORD - 100%)
- **Frame rate** : 50 fps (PAL)
- **Durée par frame** : 20 ms
- **Bits par frame** : 80 bits
- **Durée par bit** : 250 µs
- **Fréquence audio** : 2000 - 4000 Hz

### Signal LTC (PLAYBACK - 33%)
- **Frame rate apparent** : 16.67 fps
- **Durée par frame** : 60 ms (×3)
- **Bits par frame** : 80 bits (inchangé)
- **Durée par bit** : 750 µs (×3)
- **Fréquence audio** : 667 - 1333 Hz (÷3)

### Facteurs de Conversion
- **Facteur temps** : ×3
- **Facteur fréquence** : ÷3
- **Pitch shift** : -19 demi-tons
- **Timecode** : ✓ Décodable (contenu binaire inchangé)

---

## 🔬 Principe Physique

Sur la bande magnétique, le LTC est enregistré comme un **signal audio analogique** sur une piste longitudinale dédiée.

### Enregistrement (Record)
Les transitions magnétiques sont espacées de **250 µs** (à 50p).

### Lecture Ralentie (Playback 33%)
La tête de lecture parcourt la bande **3× plus lentement** → les mêmes transitions sont lues avec un espacement de **750 µs**.

### Auto-synchronisation
Le timecode reste **parfaitement décodable** car l'**encodage biphase** est auto-synchronisant — seule la fréquence change, pas le contenu binaire. C'est ce qui permet la lecture en **shuttle/jog** sur les magnétoscopes professionnels.

---

## 🚀 Utilisation

### En ligne
Visitez simplement : **https://plhfak.github.io/ltc-visualisation/**

### Localement
```bash
# Cloner le repository
git clone https://github.com/PLHFak/ltc-visualisation.git

# Ouvrir dans un navigateur
cd ltc-visualisation
open index.html
```

Aucune dépendance requise — HTML/CSS/SVG pur !

---

## 🎨 Fonctionnalités

- ✅ Visualisation SVG précise des formes d'onde LTC
- ✅ Comparaison côte à côte Record vs Playback
- ✅ Annotations techniques détaillées
- ✅ Statistiques de timing en temps réel
- ✅ Explication physique du phénomène
- ✅ Design responsive et moderne

---

## 📚 Références Techniques

### Standards
- **SMPTE 12M** : Linear Time Code (LTC) specification
- **IEC 60461** : Time and control code for video tape recorders

### Ressources
- [SMPTE Timecode - Wikipedia](https://en.wikipedia.org/wiki/SMPTE_timecode)
- [Linear Timecode (LTC) - Broadcast Engineering](https://www.broadcastengineering.com)

---

## 🛠️ Évolutions Futures

### Phase 2 : Interactivité
- [ ] Slider pour ajuster la vitesse de playback (10% → 200%)
- [ ] Animation play/pause
- [ ] Sélecteur de frame rate (25p, 50p, 60p)

### Phase 3 : Fonctionnalités Avancées
- [ ] Générateur LTC audio réel
- [ ] Analyseur de fichiers audio contenant du LTC
- [ ] Comparaison LTC vs VITC vs MTC

### Phase 4 : Optimisations
- [ ] Mode sombre/clair
- [ ] Internationalisation (EN/FR)
- [ ] Export des visualisations

---

## 👤 Auteur

**Pierre L'Hoest**  
Expert en systèmes de synchronisation broadcast et technologies vidéo professionnelles

---

## 📄 Licence

Ce projet est fourni à des fins pédagogiques et de démonstration technique.

---

## 🙏 Remerciements

Merci à la communauté broadcast pour le partage des connaissances techniques sur les systèmes de timecode et la synchronisation vidéo professionnelle.
