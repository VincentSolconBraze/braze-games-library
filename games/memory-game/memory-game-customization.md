# 🎨 Memory Game Customization Guide

This guide provides detailed instructions for customizing the Memory Game for your specific brand and campaign needs.

## 📋 Table of Contents
1. [Quick Customization](#quick-customization)
2. [Visual Customization](#visual-customization)
3. [Card Content Options](#card-content-options)
4. [Gameplay Modifications](#gameplay-modifications)
5. [Reward Systems](#reward-systems)
6. [Advanced Features](#advanced-features)
7. [Industry-Specific Examples](#industry-specific-examples)

## 🚀 Quick Customization

### 5-Minute Setup
For a quick brand customization, update these key elements:

```javascript
// 1. Change card theme (line ~380)
currentSet: 'fruits', // Change to 'animals', 'sports', or 'food'

// 2. Update colors (line ~15-25)
--primary-color: #FF6B35;      // Your brand primary
--secondary-color: #F7931E;    // Your brand secondary

// 3. Modify rewards (line ~400)
rewards: [
    { minEfficiency: 90, reward: 'YOUR_TOP_REWARD', code: 'CODE1' },
    { minEfficiency: 75, reward: 'YOUR_MID_REWARD', code: 'CODE2' },
    { minEfficiency: 60, reward: 'YOUR_LOW_REWARD', code: 'CODE3' },
    { minEfficiency: 0, reward: 'YOUR_BASE_REWARD', code: 'CODE4' }
]

// 4. Update text (in HTML)
<h1 class="game-title">Your Game Title</h1>
<p class="game-subtitle">Your subtitle message</p>
```

## 🎨 Visual Customization

### Color Schemes

#### Option 1: Gradient Backgrounds
```css
/* Elegant Purple Gradient */
--background-gradient: linear-gradient(135deg, #667eea 0%, #764ba2 100%);

/* Warm Sunset Gradient */
--background-gradient: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);

/* Cool Ocean Gradient */
--background-gradient: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);

/* Corporate Blue Gradient */
--background-gradient: linear-gradient(135deg, #2E3192 0%, #1BFFFF 100%);
```

#### Option 2: Brand-Specific Colors
```css
/* Example: Coca-Cola Theme */
:root {
    --primary-color: #F40000;
    --secondary-color: #000000;
    --accent-color: #FFFFFF;
    --card-back-gradient: linear-gradient(135deg, #F40000 0%, #8B0000 100%);
}

/* Example: Spotify Theme */
:root {
    --primary-color: #1DB954;
    --secondary-color: #191414;
    --accent-color: #FFFFFF;
    --background-gradient: linear-gradient(135deg, #191414 0%, #1DB954 100%);
}
```

### Card Styling

#### Rounded Cards
```css
.card-face {
    border-radius: 20px; /* More rounded */
}
```

#### Square Cards
```css
.card-face {
    border-radius: 4px; /* Minimal rounding */
}
```

#### Custom Card Backs
```css
.card-front {
    background-image: url('your-logo.svg');
    background-size: 60%;
    background-repeat: no-repeat;
    background-position: center;
    background-color: var(--primary-color);
}
```

## 🃏 Card Content Options

### 1. Text-Based Cards
```javascript
cardSets: {
    discounts: ['10%', '15%', '20%', '25%', '30%', '40%', '50%', 'FREE'],
    features: ['Fast', 'Secure', 'Easy', 'Smart', 'Pro', 'Plus', 'Premium', 'Elite'],
    sizes: ['XS', 'S', 'M', 'L', 'XL', 'XXL', '2XL', '3XL']
}
```

### 2. Image-Based Cards
```javascript
// Upload images to Braze Media Library first
cardSets: {
    products: [
        '<img src="{{media.product1}}" alt="Product 1">',
        '<img src="{{media.product2}}" alt="Product 2">',
        '<img src="{{media.product3}}" alt="Product 3">',
        '<img src="{{media.product4}}" alt="Product 4">',
        '<img src="{{media.product5}}" alt="Product 5">',
        '<img src="{{media.product6}}" alt="Product 6">',
        '<img src="{{media.product7}}" alt="Product 7">',
        '<img src="{{media.product8}}" alt="Product 8">'
    ]
}
```

### 3. Icon-Based Cards
```javascript
cardSets: {
    // Shopping icons
    shopping: ['🛒', '💳', '🛍️', '🏪', '💰', '🤑', '💸', '🎁'],
    
    // Travel icons
    travel: ['✈️', '🏖️', '🗺️', '🧳', '📸', '🏨', '🚕', '🎫'],
    
    // Fitness icons
    fitness: ['💪', '🏃', '🧘', '🚴', '⛹️', '🤸', '🏋️', '🤾'],
    
    // Tech icons
    tech: ['💻', '📱', '⌚', '🎮', '🖥️', '⌨️', '🖱️', '🎧']
}
```

### 4. Mixed Content
```javascript
cardSets: {
    mixed: [
        '⭐', 
        '<span style="color: gold;">VIP</span>',
        '🎯',
        '<img src="logo.png" style="width: 40px;">',
        '💎',
        '<strong>PRO</strong>',
        '🏆',
        '<em>Special</em>'
    ]
}
```

## 🎮 Gameplay Modifications

### Difficulty Variations

#### Super Easy Mode (Kids/Seniors)
```javascript
difficulties: {
    kids: { cols: 2, rows: 3, pairs: 3 },  // Only 6 cards
    easy: { cols: 3, rows: 4, pairs: 6 },
    medium: { cols: 4, rows: 4, pairs: 8 }
}
```

#### Challenge Mode
```javascript
difficulties: {
    medium: { cols: 4, rows: 4, pairs: 8 },
    hard: { cols: 5, rows: 4, pairs: 10 },
    expert: { cols: 6, rows: 5, pairs: 15 }  // 30 cards!
}
```

### Time Limits

#### Add Countdown Timer
```javascript
// Add after startGame()
let timeLimit = 60; // 60 seconds
const countdownInterval = setInterval(() => {
    timeLimit--;
    document.getElementById('timer-display').textContent = `${timeLimit}s`;
    
    if (timeLimit <= 10) {
        document.getElementById('timer-display').style.color = 'red';
    }
    
    if (timeLimit <= 0) {
        clearInterval(countdownInterval);
        endGame(false); // Time's up!
    }
}, 1000);
```

### Lives System
```javascript
let lives = 3;
let wrongMatches = 0;

function checkForMatch() {
    // ... existing code ...
    
    if (!match) {
        wrongMatches++;
        lives--;
        updateLivesDisplay();
        
        if (lives === 0) {
            endGame(false); // Game over!
        }
    }
}

function updateLivesDisplay() {
    document.getElementById('lives-display').textContent = '❤️'.repeat(lives);
}
```

## 🎁 Reward Systems

### 1. Tiered Rewards
```javascript
rewards: [
    { 
        minEfficiency: 95, 
        reward: 'PLATINUM STATUS', 
        code: 'PLAT95',
        message: 'Incredible! You\'ve earned Platinum status!'
    },
    { 
        minEfficiency: 85, 
        reward: 'GOLD STATUS', 
        code: 'GOLD85',
        message: 'Amazing! Welcome to Gold tier!'
    },
    { 
        minEfficiency: 70, 
        reward: 'SILVER STATUS', 
        code: 'SILVER70',
        message: 'Great job! You\'ve reached Silver!'
    },
    { 
        minEfficiency: 0, 
        reward: 'BRONZE STATUS', 
        code: 'BRONZE',
        message: 'Thanks for playing! Enjoy Bronze benefits!'
    }
]
```

### 2. Random Rewards
```javascript
function getRandomReward() {
    const possibleRewards = [
        { reward: '10% OFF', code: 'SAVE10', weight: 50 },
        { reward: '20% OFF', code: 'SAVE20', weight: 30 },
        { reward: '30% OFF', code: 'SAVE30', weight: 15 },
        { reward: 'FREE SHIPPING', code: 'FREESHIP', weight: 5 }
    ];
    
    // Weighted random selection
    const totalWeight = possibleRewards.reduce((sum, r) => sum + r.weight, 0);
    let random = Math.random() * totalWeight;
    
    for (const reward of possibleRewards) {
        random -= reward.weight;
        if (random <= 0) return reward;
    }
}
```

### 3. Progressive Rewards
```javascript
// Track games across sessions
let gamesPlayed = parseInt(localStorage.getItem('memoryGamesPlayed') || '0');
gamesPlayed++;

const progressiveRewards = [
    { games: 1, reward: '10% OFF', message: 'First game bonus!' },
    { games: 5, reward: '15% OFF', message: '5 games milestone!' },
    { games: 10, reward: '20% OFF', message: '10 games achievement!' },
    { games: 25, reward: '30% OFF', message: 'Memory Master status!' }
];

const currentReward = progressiveRewards.find(r => r.games === gamesPlayed) || 
                     progressiveRewards[0];
```

## 🚀 Advanced Features

### 1. Power-Ups
```javascript
const powerUps = {
    peek: {
        name: 'Peek',
        icon: '👀',
        action: () => {
            // Show all cards for 2 seconds
            document.querySelectorAll('.memory-card').forEach(card => {
                card.classList.add('flipped');
            });
            setTimeout(() => {
                document.querySelectorAll('.memory-card:not(.matched)').forEach(card => {
                    card.classList.remove('flipped');
                });
            }, 2000);
        }
    },
    
    hint: {
        name: 'Hint',
        icon: '💡',
        action: () => {
            // Highlight a matching pair
            const unmatched = Array.from(document.querySelectorAll('.memory-card:not(.matched)'));
            const card1 = unmatched[0];
            const match = unmatched.find(c => 
                c.dataset.content === card1.dataset.content && c !== card1
            );
            
            card1.style.boxShadow = '0 0 20px gold';
            match.style.boxShadow = '0 0 20px gold';
            
            setTimeout(() => {
                card1.style.boxShadow = '';
                match.style.boxShadow = '';
            }, 1000);
        }
    },
    
    freeze: {
        name: 'Freeze',
        icon: '🧊',
        action: () => {
            // Pause timer for 10 seconds
            clearInterval(gameState.timerInterval);
            setTimeout(() => startTimer(), 10000);
        }
    }
};
```

### 2. Combo System
```javascript
let combo = 0;
let comboMultiplier = 1;

function checkForMatch() {
    // ... existing code ...
    
    if (match) {
        combo++;
        comboMultiplier = Math.min(combo, 5); // Max 5x
        
        // Show combo notification
        showNotification(`${combo}x COMBO!`);
        
        // Bonus points/rewards for combos
        const bonusPoints = 100 * comboMultiplier;
    } else {
        combo = 0;
        comboMultiplier = 1;
    }
}
```

### 3. Achievement System
```javascript
const achievements = [
    { id: 'speed_demon', name: 'Speed Demon', condition: 'Complete in under 30 seconds' },
    { id: 'perfect', name: 'Perfect Memory', condition: 'Complete with 100% efficiency' },
    { id: 'persistent', name: 'Persistent', condition: 'Play 10 games' },
    { id: 'lucky', name: 'Lucky', condition: 'Get 3 matches in a row' }
];

function checkAchievements() {
    // Check and award achievements
    if (duration < 30 && !hasAchievement('speed_demon')) {
        unlockAchievement('speed_demon');
    }
}
```

## 🏢 Industry-Specific Examples

### E-commerce Fashion
```javascript
const config = {
    cardSets: {
        categories: ['👕', '👗', '👟', '👜', '👒', '🧥', '👔', '🧦'],
        brands: [
            '<img src="nike.png">',
            '<img src="adidas.png">',
            '<img src="puma.png">',
            '<img src="reebok.png">',
            // More brands
        ]
    },
    
    rewards: [
        { minEfficiency: 90, reward: '30% OFF EVERYTHING', code: 'FASHION30' },
        { minEfficiency: 75, reward: 'FREE SHIPPING + 20% OFF', code: 'STYLE20' },
        { minEfficiency: 60, reward: '15% OFF NEXT ORDER', code: 'SHOP15' },
        { minEfficiency: 0, reward: '10% OFF WELCOME', code: 'NEW10' }
    ]
};
```

### Restaurant/Food Delivery
```javascript
const config = {
    cardSets: {
        menu: ['🍕', '🍔', '🌮', '🍜', '🍣', '🥗', '🍝', '🥘'],
        desserts: ['🍰', '🍪', '🍩', '🧁', '🍮', '🍦', '🥧', '🍫']
    },
    
    rewards: [
        { minEfficiency: 90, reward: 'FREE DESSERT', code: 'SWEET' },
        { minEfficiency: 75, reward: 'FREE DELIVERY', code: 'DELIVER' },
        { minEfficiency: 60, reward: '20% OFF ORDER', code: 'HUNGRY20' },
        { minEfficiency: 0, reward: '10% OFF', code: 'TASTY10' }
    ],
    
    // Custom messaging
    text: {
        gameTitle: 'Menu Memory',
        welcomeMessage: 'Match the dishes to win delicious rewards!',
        congratsTitle: 'Bon Appétit!'
    }
};
```

### SaaS/B2B
```javascript
const config = {
    cardSets: {
        features: [
            '<i class="icon-dashboard"></i>',
            '<i class="icon-analytics"></i>',
            '<i class="icon-automation"></i>',
            '<i class="icon-integration"></i>',
            '<i class="icon-security"></i>',
            '<i class="icon-support"></i>',
            '<i class="icon-api"></i>',
            '<i class="icon-cloud"></i>'
        ]
    },
    
    rewards: [
        { minEfficiency: 90, reward: '3 MONTHS FREE', code: 'TRIAL90' },
        { minEfficiency: 75, reward: '2 MONTHS FREE', code: 'TRIAL60' },
        { minEfficiency: 60, reward: '1 MONTH FREE', code: 'TRIAL30' },
        { minEfficiency: 0, reward: '14-DAY TRIAL', code: 'TRY14' }
    ]
};
```

### Education/E-learning
```javascript
const config = {
    cardSets: {
        subjects: ['📚', '🔬', '🎨', '🎵', '💻', '🌍', '📐', '🏃'],
        languages: [
            '<span>EN</span>',
            '<span>ES</span>',
            '<span>FR</span>',
            '<span>DE</span>',
            '<span>IT</span>',
            '<span>PT</span>',
            '<span>中文</span>',
            '<span>日本</span>'
        ]
    },
    
    rewards: [
        { minEfficiency: 90, reward: 'FREE COURSE', code: 'LEARN100' },
        { minEfficiency: 75, reward: '50% OFF COURSE', code: 'LEARN50' },
        { minEfficiency: 60, reward: '30% OFF COURSE', code: 'LEARN30' },
        { minEfficiency: 0, reward: '20% OFF TRIAL', code: 'TRY20' }
    ]
};
```

## 💡 Pro Tips

### Performance Optimization
1. **Preload Images**: Upload all images to Braze Media Library
2. **Limit Animations**: Reduce on older devices
3. **Lazy Loading**: Load card content only when needed
4. **Cache Results**: Store game state for quick restarts

### Engagement Boosters
1. **Daily Challenges**: Different theme each day
2. **Leaderboards**: Show top scores
3. **Social Sharing**: Share results for bonus rewards
4. **Streaks**: Reward consecutive daily plays

### A/B Testing Ideas
1. **Card Themes**: Test which theme drives most engagement
2. **Difficulty**: Find the sweet spot for completion rates
3. **Reward Values**: Test different reward tiers
4. **Visual Styles**: Compare minimalist vs rich designs

## 🎯 Conclusion

The Memory Game is highly flexible and can be adapted to any brand or campaign goal. Start with the quick customizations, then gradually add advanced features based on your needs and user feedback.

Remember: The best customization is one that aligns with your brand while keeping the game fun and rewarding for players!