# 🎨 Flame Catcher - Customization Guide

> Complete guide to customizing the Flame Catcher game for your brand and campaigns.

## 📋 Table of Contents

1. [Visual Customization](#visual-customization)
2. [Gameplay Adjustments](#gameplay-adjustments)
3. [Reward Configuration](#reward-configuration)
4. [Content Variations](#content-variations)
5. [Advanced Modifications](#advanced-modifications)
6. [Industry Examples](#industry-examples)

---

## 🎨 Visual Customization

### Brand Colors

Replace the default colors with your brand palette:

```css
:root {
    /* Primary Brand Colors */
    --primary-color: #FF6B35;      /* Your main brand color */
    --secondary-color: #F7931E;    /* Your secondary brand color */
    --accent-color: #A333C8;       /* Accent for special elements */
    
    /* Functional Colors */
    --success-color: #21BA45;      /* Positive feedback */
    --danger-color: #DB2828;       /* Negative feedback/bombs */
    --dark-color: #1B1C1D;         /* Text and borders */
    --light-color: #FFFFFF;        /* Backgrounds */
    
    /* Game Background */
    --game-bg: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
}
```

#### Popular Color Schemes

**Midnight Theme**
```css
--primary-color: #4A90E2;
--secondary-color: #7B68EE;
--game-bg: linear-gradient(135deg, #1a1a2e 0%, #16213e 100%);
```

**Tropical Theme**
```css
--primary-color: #00CEC9;
--secondary-color: #FD79A8;
--game-bg: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
```

**Corporate Theme**
```css
--primary-color: #2C3E50;
--secondary-color: #3498DB;
--game-bg: linear-gradient(135deg, #ECF0F1 0%, #BDC3C7 100%);
```

### Character Customization

Replace the Braze flame with your mascot:

```css
#collector {
    /* Option 1: Use your own image */
    background-image: url('YOUR_MASCOT_URL_HERE');
    
    /* Option 2: Use emoji as character */
    background-image: none;
    font-size: 50px;
    display: flex;
    align-items: center;
    justify-content: center;
}
```

```javascript
// If using emoji, add this after initialization
if (!collector.style.backgroundImage) {
    collector.textContent = '🦸'; // Your emoji mascot
}
```

### Typography

Customize fonts to match your brand:

```css
/* Add to top of <style> section */
@import url('https://fonts.googleapis.com/css2?family=YourFont:wght@400;700&display=swap');

body {
    font-family: 'YourFont', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Arial, sans-serif;
}

.game-title {
    font-family: 'YourFont', sans-serif;
    font-weight: 700;
    /* Add custom styling */
    text-transform: uppercase;
    letter-spacing: 3px;
}
```

---

## 🎮 Gameplay Adjustments

### Difficulty Configurations

#### Easy Mode (Casual Players)
```javascript
const config = {
    difficulties: [
        { time: 0, dropSpeed: 1500, fallSpeed: 2.5 },
        { time: 15000, dropSpeed: 1200, fallSpeed: 2.2 },
        { time: 30000, dropSpeed: 1000, fallSpeed: 2 },
        { time: 45000, dropSpeed: 800, fallSpeed: 1.8 }
    ],
    maxLives: 7, // More forgiving
    gameDuration: 90000 // 90 seconds
};
```

#### Hard Mode (Experienced Players)
```javascript
const config = {
    difficulties: [
        { time: 0, dropSpeed: 800, fallSpeed: 1.5, simultaneous: 2 },
        { time: 5000, dropSpeed: 600, fallSpeed: 1.2, simultaneous: 3 },
        { time: 10000, dropSpeed: 400, fallSpeed: 1, simultaneous: 4 },
        { time: 20000, dropSpeed: 300, fallSpeed: 0.8, simultaneous: 5 }
    ],
    maxLives: 3, // Less forgiving
    gameDuration: 45000 // 45 seconds
};
```

#### Kids Mode
```javascript
const config = {
    difficulties: [
        { time: 0, dropSpeed: 2000, fallSpeed: 3 }
        // No progression, stays easy
    ],
    maxLives: 10,
    gameDuration: 120000, // 2 minutes
    rewards: [
        { emoji: '🍬', points: 10, weight: 50, name: 'candy' },
        { emoji: '🍭', points: 20, weight: 30, name: 'lollipop' },
        { emoji: '🧸', points: 50, weight: 20, name: 'teddy' }
        // No bombs for kids
    ]
};
```

### Game Duration Options

```javascript
// Quick play (30 seconds)
gameDuration: 30000,

// Standard (60 seconds) - Default
gameDuration: 60000,

// Extended (2 minutes)
gameDuration: 120000,

// Endless (until lives run out)
gameDuration: null, // Remove timeout
```

### Lives System Variations

```javascript
// Unlimited lives (score-based only)
maxLives: Infinity,

// One-hit challenge
maxLives: 1,

// Regenerating lives
setInterval(() => {
    if (gameState.lives < config.maxLives && gameState.active) {
        gameState.lives++;
        updateDisplay();
    }
}, 10000); // Regenerate 1 life every 10 seconds
```

---

## 🎁 Reward Configuration

### Item Types & Values

#### E-commerce Theme
```javascript
rewards: [
    { emoji: '👕', points: 10, weight: 35, name: 'shirt' },
    { emoji: '👟', points: 15, weight: 30, name: 'shoes' },
    { emoji: '👜', points: 20, weight: 20, name: 'bag' },
    { emoji: '💎', points: 50, weight: 10, name: 'jewelry' },
    { emoji: '❌', points: -20, weight: 15, name: 'return', isPenalty: true }
]
```

#### Food & Restaurant Theme
```javascript
rewards: [
    { emoji: '🍔', points: 10, weight: 30, name: 'burger' },
    { emoji: '🍕', points: 15, weight: 25, name: 'pizza' },
    { emoji: '🌮', points: 20, weight: 20, name: 'taco' },
    { emoji: '🍰', points: 30, weight: 15, name: 'dessert' },
    { emoji: '🌶️', points: -15, weight: 10, name: 'spicy', isPenalty: true }
]
```

#### Gaming Theme
```javascript
rewards: [
    { emoji: '🪙', points: 10, weight: 40, name: 'coin' },
    { emoji: '💎', points: 25, weight: 25, name: 'gem' },
    { emoji: '🏆', points: 50, weight: 15, name: 'trophy' },
    { emoji: '⚡', points: 100, weight: 5, name: 'powerup' },
    { emoji: '💀', points: -30, weight: 15, name: 'skull', isPenalty: true }
]
```

### Reward Tiers

#### Percentage-Based Rewards
```javascript
rewardTiers: [
    { minScore: 800, reward: '40% OFF', code: 'SUPER40' },
    { minScore: 600, reward: '30% OFF', code: 'GREAT30' },
    { minScore: 400, reward: '20% OFF', code: 'GOOD20' },
    { minScore: 200, reward: '10% OFF', code: 'NICE10' },
    { minScore: 0, reward: '5% OFF', code: 'PLAY5' }
]
```

#### Fixed Amount Rewards
```javascript
rewardTiers: [
    { minScore: 1000, reward: '$25 OFF', code: 'SAVE25' },
    { minScore: 750, reward: '$15 OFF', code: 'SAVE15' },
    { minScore: 500, reward: '$10 OFF', code: 'SAVE10' },
    { minScore: 250, reward: '$5 OFF', code: 'SAVE5' },
    { minScore: 0, reward: 'Free Shipping', code: 'FREESHIP' }
]
```

#### Non-Monetary Rewards
```javascript
rewardTiers: [
    { minScore: 1000, reward: 'VIP Status', code: 'VIPACCESS' },
    { minScore: 750, reward: 'Early Access', code: 'EARLY24' },
    { minScore: 500, reward: 'Bonus Points', code: 'POINTS2X' },
    { minScore: 250, reward: 'Free Sample', code: 'TRYIT' },
    { minScore: 0, reward: 'Thank You', code: 'THANKS' }
]
```

---

## 📝 Content Variations

### Text Customization

#### Casual/Fun Tone
```html
<h1 class="game-title">🎮 Catch 'Em All!</h1>
<p class="game-subtitle">Snag the goodies, dodge the baddies!</p>
<button class="start-button">LET'S GO!</button>

<!-- Game Over -->
<h2 class="game-over-title">💥 Boom! Nice Run!</h2>
```

#### Professional Tone
```html
<h1 class="game-title">Rewards Challenge</h1>
<p class="game-subtitle">Collect points to unlock exclusive offers</p>
<button class="start-button">Begin Challenge</button>

<!-- Game Over -->
<h2 class="game-over-title">Challenge Complete</h2>
```

#### Seasonal Themes

**Holiday Season**
```javascript
// Christmas Theme
rewards: [
    { emoji: '🎁', points: 20, weight: 30, name: 'gift' },
    { emoji: '⭐', points: 30, weight: 25, name: 'star' },
    { emoji: '🎅', points: 50, weight: 15, name: 'santa' },
    { emoji: '❄️', points: 10, weight: 20, name: 'snowflake' },
    { emoji: '🌨️', points: -20, weight: 10, name: 'blizzard', isPenalty: true }
]
```

**Halloween Theme**
```javascript
rewards: [
    { emoji: '🍬', points: 10, weight: 35, name: 'candy' },
    { emoji: '🎃', points: 20, weight: 25, name: 'pumpkin' },
    { emoji: '👻', points: 30, weight: 20, name: 'ghost' },
    { emoji: '🦇', points: 50, weight: 10, name: 'bat' },
    { emoji: '🕷️', points: -25, weight: 10, name: 'spider', isPenalty: true }
]
```

### Language Localization

```javascript
const translations = {
    en: {
        title: '🔥 Flame Catcher',
        subtitle: 'Catch rewards and boost your score!',
        playButton: 'PLAY NOW!',
        score: 'Score',
        lives: 'Lives',
        gameOver: '🎉 Great Job!',
        playAgain: 'Play Again',
        claimReward: 'Claim Reward'
    },
    es: {
        title: '🔥 Atrapa Llamas',
        subtitle: '¡Atrapa recompensas y aumenta tu puntuación!',
        playButton: '¡JUGAR AHORA!',
        score: 'Puntos',
        lives: 'Vidas',
        gameOver: '🎉 ¡Buen Trabajo!',
        playAgain: 'Jugar de Nuevo',
        claimReward: 'Reclamar Premio'
    },
    fr: {
        title: '🔥 Attrapeur de Flammes',
        subtitle: 'Attrapez des récompenses et boostez votre score!',
        playButton: 'JOUER MAINTENANT!',
        score: 'Score',
        lives: 'Vies',
        gameOver: '🎉 Excellent!',
        playAgain: 'Rejouer',
        claimReward: 'Réclamer la Récompense'
    }
};

// Apply translations
const lang = 'es'; // or detect from user
document.querySelector('.game-title').textContent = translations[lang].title;
// ... apply other translations
```

---

## 🚀 Advanced Modifications

### Power-Up System

```javascript
// Add power-ups to rewards
rewards: [
    // ... regular rewards ...
    { emoji: '🛡️', points: 0, weight: 5, name: 'shield', isPowerUp: true },
    { emoji: '🧲', points: 0, weight: 5, name: 'magnet', isPowerUp: true },
    { emoji: '⏰', points: 0, weight: 3, name: 'slowtime', isPowerUp: true }
]

// Power-up handlers
const powerUps = {
    shield: {
        duration: 5000,
        activate: () => {
            gameState.invulnerable = true;
            collector.style.border = '3px solid gold';
            setTimeout(() => {
                gameState.invulnerable = false;
                collector.style.border = 'none';
            }, 5000);
        }
    },
    magnet: {
        duration: 3000,
        activate: () => {
            gameState.magnetActive = true;
            // Items get attracted to collector
            setTimeout(() => {
                gameState.magnetActive = false;
            }, 3000);
        }
    },
    slowtime: {
        duration: 4000,
        activate: () => {
            // Slow down falling speed
            const currentDifficulty = config.difficulties[gameState.currentDifficulty];
            currentDifficulty.fallSpeed *= 2;
            setTimeout(() => {
                currentDifficulty.fallSpeed /= 2;
            }, 4000);
        }
    }
};
```

### Combo System

```javascript
// Track consecutive catches
let combo = 0;
let comboTimer;

function collectItem(item) {
    const points = parseInt(item.dataset.points);
    
    if (points > 0) {
        combo++;
        clearTimeout(comboTimer);
        
        // Reset combo after 2 seconds of no collection
        comboTimer = setTimeout(() => {
            combo = 0;
        }, 2000);
        
        // Apply combo multiplier
        const multiplier = Math.min(combo, 5); // Max 5x
        const totalPoints = points * multiplier;
        
        if (multiplier > 1) {
            showComboText(`${multiplier}x COMBO!`);
        }
        
        gameState.score += totalPoints;
    } else {
        combo = 0; // Reset on bomb
    }
    
    updateDisplay();
}
```

### Achievement System

```javascript
const achievements = {
    firstCatch: {
        name: 'First Catch',
        description: 'Catch your first item',
        check: () => gameState.totalCatches === 1,
        reward: 50
    },
    survivor: {
        name: 'Survivor',
        description: 'Survive for 30 seconds',
        check: () => Date.now() - gameState.startTime > 30000,
        reward: 100
    },
    perfectRun: {
        name: 'Perfect Run',
        description: 'Complete a game without hitting bombs',
        check: () => gameState.bombsHit === 0 && !gameState.active,
        reward: 200
    },
    highScorer: {
        name: 'High Scorer',
        description: 'Score over 1000 points',
        check: () => gameState.score > 1000,
        reward: 150
    }
};

// Check achievements after each action
function checkAchievements() {
    Object.entries(achievements).forEach(([key, achievement]) => {
        if (!achievement.unlocked && achievement.check()) {
            achievement.unlocked = true;
            showAchievement(achievement);
            gameState.score += achievement.reward;
            
            if (typeof brazeBridge !== 'undefined') {
                brazeBridge.logCustomEvent('achievement_unlocked', {
                    achievement: key,
                    reward: achievement.reward
                });
            }
        }
    });
}
```

### Dynamic Backgrounds

```javascript
// Change background based on score
function updateBackground() {
    const gameContainer = document.getElementById('game-container');
    
    if (gameState.score < 100) {
        gameContainer.style.background = 'linear-gradient(135deg, #667eea 0%, #764ba2 100%)';
    } else if (gameState.score < 300) {
        gameContainer.style.background = 'linear-gradient(135deg, #f093fb 0%, #f5576c 100%)';
    } else if (gameState.score < 500) {
        gameContainer.style.background = 'linear-gradient(135deg, #fa709a 0%, #fee140 100%)';
    } else {
        gameContainer.style.background = 'linear-gradient(135deg, #a8edea 0%, #fed6e3 100%)';
    }
}
```

---

## 🏢 Industry Examples

### Retail/E-commerce

```javascript
// Black Friday Theme
const config = {
    rewards: [
        { emoji: '🏷️', points: 10, weight: 30, name: 'tag' },
        { emoji: '🛍️', points: 20, weight: 25, name: 'bag' },
        { emoji: '💸', points: 30, weight: 20, name: 'cash' },
        { emoji: '🎁', points: 50, weight: 15, name: 'gift' },
        { emoji: '⏰', points: -25, weight: 10, name: 'timeout', isPenalty: true }
    ],
    rewardTiers: [
        { minScore: 800, reward: 'BOGO Deal', code: 'BOGO2024' },
        { minScore: 600, reward: '50% OFF', code: 'FRIDAY50' },
        { minScore: 400, reward: '35% OFF', code: 'SAVE35' },
        { minScore: 200, reward: '20% OFF', code: 'DEAL20' },
        { minScore: 0, reward: '10% OFF', code: 'WELCOME10' }
    ]
};
```

### Fitness/Wellness

```javascript
// Fitness Challenge Theme
const config = {
    rewards: [
        { emoji: '💪', points: 10, weight: 30, name: 'muscle' },
        { emoji: '🏃', points: 15, weight: 25, name: 'runner' },
        { emoji: '🧘', points: 20, weight: 20, name: 'yoga' },
        { emoji: '🏆', points: 50, weight: 10, name: 'trophy' },
        { emoji: '🍔', points: -20, weight: 15, name: 'junkfood', isPenalty: true }
    ],
    rewardTiers: [
        { minScore: 1000, reward: '1 Month Free', code: 'FIT30DAYS' },
        { minScore: 750, reward: '2 Weeks Free', code: 'FIT14DAYS' },
        { minScore: 500, reward: '1 Week Free', code: 'FIT7DAYS' },
        { minScore: 250, reward: 'Free Class', code: 'FREECLASS' },
        { minScore: 0, reward: 'Day Pass', code: 'DAYPASS' }
    ]
};
```

### Education/EdTech

```javascript
// Learning Game Theme
const config = {
    rewards: [
        { emoji: '📚', points: 10, weight: 30, name: 'book' },
        { emoji: '✏️', points: 15, weight: 25, name: 'pencil' },
        { emoji: '🎓', points: 25, weight: 20, name: 'graduation' },
        { emoji: '💡', points: 50, weight: 10, name: 'idea' },
        { emoji: '❌', points: -20, weight: 15, name: 'wrong', isPenalty: true }
    ],
    rewardTiers: [
        { minScore: 1000, reward: 'Free Course', code: 'LEARN100' },
        { minScore: 750, reward: '50% OFF Course', code: 'LEARN50' },
        { minScore: 500, reward: '30% OFF Course', code: 'LEARN30' },
        { minScore: 250, reward: 'Free Lesson', code: 'TRYME' },
        { minScore: 0, reward: 'Study Guide', code: 'GUIDE' }
    ]
};
```

### Travel/Hospitality

```javascript
// Travel Theme
const config = {
    rewards: [
        { emoji: '✈️', points: 20, weight: 25, name: 'plane' },
        { emoji: '🏖️', points: 15, weight: 30, name: 'beach' },
        { emoji: '🗺️', points: 10, weight: 25, name: 'map' },
        { emoji: '🏝️', points: 50, weight: 10, name: 'island' },
        { emoji: '🌧️', points: -25, weight: 10, name: 'rain', isPenalty: true }
    ],
    rewardTiers: [
        { minScore: 1000, reward: '$200 OFF', code: 'FLY200' },
        { minScore: 750, reward: '$100 OFF', code: 'FLY100' },
        { minScore: 500, reward: '$50 OFF', code: 'FLY50' },
        { minScore: 250, reward: 'Priority Check-in', code: 'PRIORITY' },
        { minScore: 0, reward: 'Travel Guide', code: 'GUIDE' }
    ]
};
```

---

## 📝 Testing Your Customizations

### Pre-Launch Checklist

- [ ] Test on all target devices
- [ ] Verify analytics tracking
- [ ] Check reward tier progression
- [ ] Validate all text content
- [ ] Test offline functionality
- [ ] Verify performance (< 50KB)
- [ ] Check accessibility features (keyboard nav, zoom support)
- [ ] Test with real user accounts
- [ ] Verify reward codes work
- [ ] Test edge cases (0 score, max score)

### A/B Testing Ideas

1. **Difficulty Levels**: Test easy vs normal vs hard
2. **Game Duration**: 30s vs 60s vs 90s
3. **Reward Values**: Higher discounts vs more tiers
4. **Visual Themes**: Bright vs dark themes
5. **Character Types**: Mascot vs emoji vs custom
6. **Sound Effects**: With vs without sounds
7. **Power-ups**: Enabled vs disabled
8. **Lives Count**: 3 vs 5 vs unlimited

---

Need more customization help? Check the main [Braze Games Library](https://github.com/VincentSolconBraze/braze-games-library) documentation!