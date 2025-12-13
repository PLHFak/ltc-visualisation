# 📐 Notes Techniques - LTC (Linear Time Code)

## 🎯 Spécifications SMPTE 12M

Le **Linear Time Code (LTC)** est un standard SMPTE pour l'encodage du timecode sous forme de signal audio.

### Structure d'une Frame LTC

Chaque frame LTC contient **80 bits** :
- **26 bits** : Timecode (heures, minutes, secondes, frames)
- **32 bits** : User bits (données utilisateur)
- **16 bits** : Sync word (mot de synchronisation)
- **6 bits** : Flags (drop frame, color frame, etc.)

### Encodage Biphase Mark

Le LTC utilise un encodage **biphase mark** (Manchester) :
- **Bit 0** : Une transition au milieu de la période
- **Bit 1** : Deux transitions (début + milieu)

**Avantage** : Auto-synchronisant — pas besoin d'horloge séparée.

---

## ⏱️ Calculs de Timing

### Configuration de Base (50p PAL)

**Frame rate** : 50 fps  
**Durée par frame** : 1/50 = 20 ms  
**Bits par frame** : 80 bits  
**Durée par bit** : 20 ms / 80 = 250 µs

### Fréquences Audio

Le LTC génère des fréquences audio variables :
- **Bit 0** : 1 transition → f = 1/(2 × 250µs) = **2000 Hz**
- **Bit 1** : 2 transitions → f = 1/(250µs) = **4000 Hz**

**Plage** : 2000 - 4000 Hz (pour 50p)

---

## 🎚️ Effet du Ralentissement (33%)

### Facteur de Vitesse : ×0.33

Lorsque la bande est lue à **33% de la vitesse normale** :

#### Temps
- **Durée par frame** : 20 ms × 3 = **60 ms**
- **Durée par bit** : 250 µs × 3 = **750 µs**
- **Frame rate apparent** : 50 fps ÷ 3 = **16.67 fps**

#### Fréquences
- **Bit 0** : 2000 Hz ÷ 3 = **667 Hz**
- **Bit 1** : 4000 Hz ÷ 3 = **1333 Hz**
- **Plage** : 667 - 1333 Hz

#### Pitch Shift
Formule : `pitch_shift = 12 × log₂(ratio)`

```
pitch_shift = 12 × log₂(0.33)
            = 12 × (-1.599)
            = -19.19 demi-tons
```

**Résultat** : Le signal audio est **19 demi-tons plus grave**.

---

## 🔬 Physique de la Bande Magnétique

### Enregistrement (Record)

1. **Signal électrique** → Tête d'enregistrement
2. **Champ magnétique** → Particules magnétiques sur la bande
3. **Transitions** espacées de 250 µs (à 50p)

### Lecture (Playback)

1. **Tête de lecture** parcourt la bande
2. **Variations du champ magnétique** → Signal électrique
3. **Vitesse de lecture** détermine l'espacement temporel

#### Vitesse Normale (100%)
- Espacement : **250 µs**
- Fréquence : **2000-4000 Hz**

#### Vitesse Ralentie (33%)
- Espacement : **750 µs** (×3)
- Fréquence : **667-1333 Hz** (÷3)

### Décodabilité

**Question** : Pourquoi le timecode reste-t-il décodable ?

**Réponse** : L'encodage **biphase mark** est **auto-synchronisant** :
- Chaque bit contient sa propre horloge (transitions)
- Le décodeur s'adapte automatiquement à la fréquence
- Seul le **pattern de transitions** compte, pas leur vitesse absolue

**Analogie** : Comme lire un code Morse ralenti — les points et les traits sont plus longs, mais le message reste identique.

---

## 📊 Tableau Comparatif

| Paramètre | Record (100%) | Playback (33%) | Facteur |
|-----------|---------------|----------------|---------|
| Frame rate | 50 fps | 16.67 fps | ÷3 |
| Durée/frame | 20 ms | 60 ms | ×3 |
| Durée/bit | 250 µs | 750 µs | ×3 |
| Fréquence min | 2000 Hz | 667 Hz | ÷3 |
| Fréquence max | 4000 Hz | 1333 Hz | ÷3 |
| Pitch shift | 0 | -19 demi-tons | -19 |
| Timecode | Décodable | Décodable | ✓ |
| Bits/frame | 80 | 80 | = |

---

## 🎬 Applications Pratiques

### Shuttle/Jog sur Magnétoscopes

Les magnétoscopes professionnels permettent de lire la bande à vitesse variable :
- **Shuttle** : Lecture rapide (×2, ×4, ×8...)
- **Jog** : Lecture image par image
- **Slow motion** : Lecture ralentie (×0.5, ×0.25...)

Le **LTC reste décodable** dans tous ces modes grâce à l'auto-synchronisation.

### Limites Pratiques

**Vitesses extrêmes** :
- **Trop lent** (< 10%) : Signal trop grave, peut sortir de la bande passante audio
- **Trop rapide** (> 500%) : Signal trop aigu, distorsion possible

**Plage typique** : 10% - 200% de la vitesse normale

### Comparaison avec VITC

**VITC (Vertical Interval Time Code)** :
- Encodé dans les lignes de blanking vidéo
- **Non décodable** en lecture rapide/ralentie
- Nécessite une image vidéo stable

**LTC** :
- Encodé sur piste audio
- **Décodable** à toutes vitesses
- Indépendant de la vidéo

**Conclusion** : Le LTC est **essentiel** pour le shuttle/jog.

---

## 🔗 Références

### Standards
- **SMPTE 12M-1999** : Television, Audio and Film — Time and Control Code
- **IEC 60461** : Time and control code for video tape recorders
- **EBU Tech 3097** : Specification of the EBU Timecode

### Ressources
- [SMPTE Timecode - Wikipedia](https://en.wikipedia.org/wiki/SMPTE_timecode)
- [Linear Timecode Explained - Broadcast Engineering](https://www.broadcastengineering.com)
- [Biphase Mark Code - Wikipedia](https://en.wikipedia.org/wiki/Differential_Manchester_encoding)

---

## 📝 Notes de Calcul

### Formules Utiles

**Durée par bit** :
```
bit_duration = frame_duration / 80
```

**Fréquence LTC** :
```
f_min = 1 / (2 × bit_duration)  # Bit 0
f_max = 1 / bit_duration         # Bit 1
```

**Pitch shift** :
```
pitch_shift = 12 × log₂(speed_ratio)
```

### Exemple de Calcul (25p → 50p)

**Passage de 25 fps à 50 fps** :

```
Durée/frame (25p) = 1/25 = 40 ms
Durée/frame (50p) = 1/50 = 20 ms

Durée/bit (25p) = 40/80 = 500 µs
Durée/bit (50p) = 20/80 = 250 µs

Fréquence (25p) = 1000 - 2000 Hz
Fréquence (50p) = 2000 - 4000 Hz
```

**Conclusion** : Le LTC à 50p est **une octave plus aigu** que le LTC à 25p.
