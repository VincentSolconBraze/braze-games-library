# 🎯 Guide de Personnalisation - Spin the Wheel Braze

## 📊 Vue d'ensemble du jeu

Le **Spin the Wheel** est un jeu de chance interactif qui permet d'offrir des récompenses instantanées à vos utilisateurs. C'est un excellent outil pour :
- 🛒 Augmenter les conversions (codes promo)
- 📧 Collecter des emails (incentive pour s'inscrire)
- 🔄 Améliorer la rétention (récompenses régulières)
- 📈 Booster l'engagement (gamification)

## 🎨 Personnalisation Visuelle

### 1. **Couleurs de la marque** 
Modifiez les variables CSS au début du code :

```css
:root {
    --primary-color: #FF6B35;      /* Couleur principale */
    --secondary-color: #F7931E;    /* Couleur secondaire */
    --accent-color: #FCEE21;       /* Couleur d'accent */
    --dark-color: #2C3E50;         /* Texte foncé */
    --light-color: #FFFFFF;        /* Fond clair */
}
```

### 2. **Couleurs des segments**
Personnalisez chaque segment de la roue :

```css
.segment:nth-child(1) .segment-inner { background: #FF6B35; }
.segment:nth-child(2) .segment-inner { background: #F7931E; }
/* ... jusqu'à 8 segments */
```

### 3. **Textes et messages**
Modifiez directement dans le HTML :

```html
<h1>Spin & Win!</h1>                    <!-- Titre principal -->
<p>Try your luck and win amazing prizes!</p>  <!-- Sous-titre -->
<button>SPIN TO WIN!</button>            <!-- Texte du bouton -->
```

## 🎁 Configuration des Récompenses

### Structure d'une récompense
Chaque récompense dans le tableau JavaScript contient :

```javascript
{
    text: "20% OFF",           // Texte affiché sur la roue
    emoji: "🎯",              // Emoji dans le résultat
    code: "SAVE20",           // Code promo généré
    message: "Save 20% on..." // Message de félicitations
}
```

### Exemples de récompenses par industrie

#### 🛍️ **E-commerce**
```javascript
{ text: "30% OFF", code: "MEGA30", message: "30% off your entire order!" },
{ text: "FREE SHIP", code: "SHIP0", message: "Free shipping, no minimum!" },
{ text: "$10 OFF", code: "SAVE10", message: "$10 off orders over $50!" }
```

#### 🍔 **Restaurant/Food**
```javascript
{ text: "FREE APPETIZER", code: "FREEAPP", message: "Free appetizer with any entrée!" },
{ text: "BOGO MEAL", code: "BOGO", message: "Buy one meal, get one free!" },
{ text: "20% OFF", code: "DINE20", message: "20% off your next visit!" }
```

#### 🎮 **Gaming/App**
```javascript
{ text: "500 COINS", code: "COINS500", message: "500 bonus coins added!" },
{ text: "PREMIUM 7D", code: "PREMIUM7", message: "7 days of premium access!" },
{ text: "RARE ITEM", code: "RAREGET", message: "Unlock a rare item!" }
```

## 📈 Métriques et Analytics

### Événements trackés automatiquement :

| Événement | Description | Données collectées |
|-----------|-------------|-------------------|
| `spin_wheel_game_opened` | Ouverture du jeu | timestamp |
| `wheel_spin_started` | Clic sur SPIN | spin_count |
| `wheel_spin_completed` | Fin de rotation | reward_won, reward_code |
| `reward_displayed` | Affichage résultat | reward_type, reward_code |
| `reward_claimed` | Clic sur Claim | total_spins, game_duration |
| `game_closed` | Fermeture du jeu | total_duration, last_action |

### Attributs utilisateur mis à jour :
- `last_spin_reward` : Dernier code gagné
- `total_spins` : Nombre total de spins
- `games_completed` : Jeux terminés (incrémenté)

## 🔧 Options Avancées

### 1. **Probabilités pondérées** (optionnel)
Pour contrôler les chances de gagner :

```javascript
// Ajouter des poids aux récompenses
const rewards = [
    { text: "10% OFF", weight: 40 },    // 40% de chances
    { text: "50% OFF", weight: 5 },     // 5% de chances
    { text: "FREE SHIP", weight: 20 },  // 20% de chances
    // etc.
];
```

### 2. **Limite de spins**
Limiter le nombre de tentatives :

```javascript
const MAX_SPINS = 3;
if (spinCount >= MAX_SPINS) {
    spinBtn.textContent = "No more spins!";
    spinBtn.disabled = true;
}
```

### 3. **Timer de validité**
Ajouter une urgence :

```javascript
// Afficher "Expires in 10 minutes" dans le modal
setTimeout(() => {
    brazeBridge.logCustomEvent("reward_expired");
    closeGame();
}, 600000); // 10 minutes
```

## 📱 Adaptation Mobile

Le jeu s'adapte automatiquement mais vous pouvez ajuster :

```css
@media (max-width: 480px) {
    .wheel-container {
        width: 250px;  /* Taille sur mobile */
        height: 250px;
    }
}
```

## ⚡ Performance

### Poids du fichier
- HTML + CSS + JS : ~15KB
- Limite Braze : 200KB
- Marge pour images/fonts : ~185KB

### Optimisations possibles
1. **Réduire les segments** : 6 au lieu de 8
2. **Simplifier les animations** : Réduire les confettis
3. **Compresser le CSS** : Utiliser un minifier

## 🚀 Déploiement dans Braze

### 1. **Création de la campagne**
- Type : In-App Message
- Message Type : Custom Code
- Custom Type : HTML Upload with Preview

### 2. **Configuration du ciblage**
Exemples de segments :
- Nouveaux utilisateurs (< 7 jours)
- Utilisateurs inactifs (> 30 jours)
- VIP/Premium users
- Panier abandonné

### 3. **Déclencheurs recommandés**
- À l'ouverture de l'app
- Après X sessions
- Sur page spécifique
- Événement custom

## 💡 Bonnes Pratiques

### ✅ **À FAIRE**
- Tester sur iOS et Android
- Limiter à 1-3 spins max
- Offrir de vraies récompenses
- Tracker les conversions
- A/B tester les récompenses

### ❌ **À ÉVITER**
- Trop de segments (max 8)
- Récompenses impossibles
- Forcer trop souvent
- Oublier l'expiration
- Négliger le mobile

## 🎯 Exemples de KPIs

| Métrique | Objectif | Calcul |
|----------|----------|--------|
| Taux de spin | > 70% | spins / ouvertures |
| Taux de claim | > 60% | claims / spins gagnants |
| Conversion | > 20% | achats / claims |
| Temps moyen | 30-60s | durée moyenne session |

## 🛠️ Troubleshooting

### "Le jeu ne s'affiche pas"
- Vérifier SDK minimum requis
- Confirmer `allowUserSuppliedJavascript: true`
- Tester le type "HTML Upload with Preview"

### "Les événements ne remontent pas"
- Vérifier que `brazeBridge` est disponible
- Attendre l'event "ab.BridgeReady"
- Appeler `requestImmediateDataFlush()`

### "Performance lente"
- Réduire le nombre de confettis
- Optimiser les images
- Minifier le code

## 📞 Support

Pour toute question sur l'implémentation :
1. Consulter la doc Braze : [HTML In-App Messages](https://www.braze.com/docs)
2. Tester dans le Preview Braze
3. Vérifier la console JavaScript

---

**💪 Astuce Pro** : Commencez simple avec 10-20% de réduction, puis augmentez progressivement les récompenses selon les résultats!