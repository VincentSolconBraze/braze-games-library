# 🧠 Memory Game - Braze In-App Game

> A classic card-matching memory game with customizable themes, difficulty levels, and instant rewards, optimized for Braze in-app messages.

![Memory Game Preview](https://cdn.braze.eu/appboy/communication/assets/image_assets/images/memory-game-preview.png)

## ✨ Features

- 🃏 **Classic Memory Card Matching** - Timeless gameplay that everyone knows
- 🎯 **3 Difficulty Levels** - Easy (3×4), Medium (4×4), Hard (4×5)
- 🎨 **4 Built-in Themes** - Fruits, Animals, Sports, Food icons
- 📊 **Progress Tracking** - Real-time timer, moves counter, and progress bar
- 🏆 **Performance-Based Rewards** - Better efficiency = Better rewards
- 📱 **Fully Responsive** - Perfect on all devices
- ♿ **Accessible** - Full keyboard navigation and screen reader support
- 📈 **Complete Analytics** - Detailed event tracking for optimization
- 🚀 **Lightweight** - Only ~15KB total size
- 🔌 **No Dependencies** - Pure HTML/CSS/JavaScript

## 🚀 Quick Start

1. Copy the content of `memory-game-index.html`
2. In Braze Dashboard:
   - Create new In-App Message
   - Select "Custom Code"
   - Choose "HTML Upload with Preview"
   - Paste the code
3. Customize theme and rewards
4. Test & Launch!

## 🎨 Customization

### Colors

Edit the CSS variables at the top of the file:

```css
:root {
    --primary-color: #FF6B35;      /* Main brand color */
    --secondary-color: #F7931E;    /* Secondary brand color */
    --accent-color: #A333C8;       /* Accent for special elements */
    --success-color: #21BA45;      /* Success/match color */
    --dark-color: #1B1C1D;         /* Text color */
}
```

### Card Themes

The game includes 4 built-in themes. Change the `currentSet` in the config:

```javascript
const config = {
    cardSets: {
        fruits: ['🍎', '🍊', '🍇', '🍓', '🍒', '🥝', '🍑', '🥭', '🍍', '🥥'],
        animals: ['🐶', '🐱', '🐭', '🐹', '🦊', '🐻', '🐼', '🦁', '🐸', '🐵'],
        sports: ['⚽', '🏀', '🏈', '⚾', '🎾', '🏐', '🏓', '🏸', '🥊', '🎯'],
        food: ['🍕', '🍔', '🌮', '🍿', '🍩', '🧁', '🍪', '🍦', '☕', '🥤']
    },
    currentSet: 'fruits' // Change this to 'animals', 'sports', or 'food'
};
```

### Custom Card Content

Create your own theme with any content:

```javascript
// Text-based cards
cardSets: {
    discounts: ['10%', '15%', '20%', '25%', '30%', 'FREE', 'BOGO', '50%']
}

// Product images (upload to Braze Media Library first)
cardSets: {
    products: [
        '<img src="product1.jpg" alt="Shoes">',
        '<img src="product2.jpg" alt="Shirt">',
        // More products...
    ]
}

// Brand elements
cardSets: {
    brand: ['👕', '👟', '👜', '⌚', '🕶️', '💄', '💍', '🎩']
}
```

### Difficulty Levels

Adjust grid sizes and pair counts:

```javascript
difficulties: {
    easy: { cols: 3, rows: 4, pairs: 6 },    // 12 cards
    medium: { cols: 4, rows: 4, pairs: 8 },  // 16 cards
    hard: { cols: 4, rows: 5, pairs: 10 }    // 20 cards
}
```

### Rewards Configuration

Set rewards based on efficiency (perfect moves / actual moves):

```javascript
rewards: [
    { minEfficiency: 90, reward: '30% OFF', code: 'MASTER30' },
    { minEfficiency: 75, reward: '25% OFF', code: 'GREAT25' },
    { minEfficiency: 60, reward: '20% OFF', code: 'GOOD20' },
    { minEfficiency: 0, reward: '15% OFF', code: 'PLAY15' }
]
```

### Text Content

Update game text in the HTML:

```html
<h1 class="game-title">Memory Master</h1>
<p class="game-subtitle">Match all the pairs as quickly as possible!</p>
<h2 class="completion-title">Congratulations!</h2>
<button>Start Game</button>
```

## 📊 Analytics Events

The game automatically tracks:

| Event | When Triggered | Data Included |
|-------|----------------|---------------|
| `memory_game_opened` | Game loads | session_id, timestamp |
| `memory_game_started` | User starts game | difficulty, card_theme |
| `memory_card_flipped` | Card is flipped | card_index, card_content, flip_count |
| `memory_match_found` | Pair is matched | moves_count, matched_pairs, content |
| `memory_game_completed` | All pairs matched | duration, moves, efficiency, reward |
| `memory_reward_claimed` | Reward claimed | reward_type, reward_code, session_duration |
| `memory_game_closed` | Game closes | session_duration, had_win |

### Click Tracking

- `start_game` - Start button
- `difficulty_easy/medium/hard` - Difficulty selection
- `card_0` through `card_19` - Individual card clicks
- `play_again` - Play again button
- `claim_reward` - Claim reward button
- `close_button` - Close game

### User Attributes Updated

- `memory_games_completed` - Total games finished (incremented)
- `last_memory_efficiency` - Efficiency percentage of last game
- `last_memory_reward` - Most recent reward code earned

## 🛠️ Advanced Customization

### Time-Based Challenges

Add time pressure for bonus rewards:

```javascript
// Add countdown timer
let countdown = 60; // 60 seconds
const countdownInterval = setInterval(() => {
    countdown--;
    if (countdown <= 0) {
        endGame(false); // Time's up!
    }
}, 1000);

// Bonus for fast completion
if (duration < 30) {
    reward = upgradedReward;
}
```

### Progressive Difficulty

Unlock harder levels as players succeed:

```javascript
function unlockNextDifficulty() {
    if (gameState.difficulty === 'easy' && efficiency > 80) {
        document.querySelector('[data-level="medium"]').classList.add('unlocked');
    }
}
```

### Themed Variations

#### Holiday Theme
```javascript
cardSets: {
    christmas: ['🎅', '🎄', '🎁', '⛄', '🔔', '⭐', '🕯️', '❄️', '🦌', '🍪'],
    halloween: ['🎃', '👻', '🦇', '🕷️', '🕸️', '🧙', '⚰️', '🧛', '💀', '🌙']
}
```

#### E-commerce Theme
```javascript
cardSets: {
    categories: ['👕', '👟', '💻', '📱', '🎮', '📚', '🏠', '⚽', '💄', '🍕']
}
```

### Multi-Language Support

```javascript
const translations = {
    en: {
        title: 'Memory Master',
        start: 'Start Game',
        congrats: 'Congratulations!'
    },
    es: {
        title: 'Maestro de Memoria',
        start: 'Iniciar Juego',
        congrats: '¡Felicitaciones!'
    }
};
```

### Sound Effects

```javascript
const sounds = {
    flip: new Audio('data:audio/wav;base64,...'),
    match: new Audio('data:audio/wav;base64,...'),
    win: new Audio('data:audio/wav;base64,...')
};

// Play on card flip
sounds.flip.play();
```

## 🎯 Use Cases

### E-commerce
- **Product Discovery**: Use product images as cards
- **Category Learning**: Match products to categories
- **Seasonal Sales**: Holiday-themed memory games
- **Loyalty Rewards**: Unlock tier benefits

### Gaming/Apps
- **Tutorial Gamification**: Learn app features
- **Daily Challenges**: Different theme each day
- **Achievement System**: Unlock badges
- **Premium Content**: Win in-game currency

### Education
- **Language Learning**: Match words to images
- **Brand Education**: Learn product features
- **Training Gamification**: Employee onboarding
- **Knowledge Retention**: Quiz reinforcement

### Restaurants/Retail
- **Menu Discovery**: Match dishes to names
- **Store Locations**: Learn store layouts
- **Ingredient Education**: Food pairing game
- **Special Offers**: Time-limited rewards

## 🐛 Troubleshooting

### Cards don't flip
- Check if JavaScript is enabled
- Verify no CSS conflicts
- Test touch events on mobile
- Check `isProcessing` state

### Timer not updating
- Ensure `setInterval` is supported
- Check for performance issues
- Verify timer element exists

### Wrong difficulty showing
- Check grid CSS calculation
- Verify card array length
- Test responsive breakpoints

### Analytics not tracking
- Confirm `brazeBridge` is available
- Wait for "ab.BridgeReady" event
- Check event names match dashboard
- Use `requestImmediateDataFlush()`

### Performance issues
- Reduce animation complexity
- Limit card count on mobile
- Optimize image sizes
- Test on target devices

## 📱 Browser Support

- ✅ Chrome/Edge 80+
- ✅ Safari 13+
- ✅ Firefox 75+
- ✅ iOS Safari 13+
- ✅ Chrome Android 80+

## 🎮 Game Mechanics

### Scoring System
- **Efficiency**: Perfect moves ÷ Actual moves × 100
- **Time Bonus**: Faster completion = Higher rating
- **Streak Bonus**: Consecutive matches without mistakes
- **Difficulty Multiplier**: Harder levels = Better rewards

### Memory Strategies
- **Systematic Approach**: Flip cards in order
- **Pattern Recognition**: Remember card positions
- **Chunking**: Group related cards mentally
- **Repetition**: Multiple plays improve performance

### Difficulty Progression
1. **Easy (3×4)**: 6 pairs, good for beginners
2. **Medium (4×4)**: 8 pairs, standard challenge  
3. **Hard (4×5)**: 10 pairs, memory masters only

## 💡 Best Practices

### Performance
- Preload images in Media Library
- Minimize animation on low-end devices
- Use CSS transforms for smooth flips
- Debounce rapid clicks

### Engagement
- Start with Easy difficulty
- Offer meaningful rewards
- Show clear progress indicators
- Celebrate victories with animation

### Accessibility
- High contrast card faces
- Clear focus indicators
- Keyboard navigation
- Screen reader announcements

## 🎨 Design Tips

### Visual Hierarchy
1. Timer and moves prominent
2. Cards clearly distinguishable
3. Progress bar visible
4. Reward highlighted on completion

### Color Psychology
- **Green**: Success, matches found
- **Orange/Red**: Energy, excitement
- **Blue/Purple**: Trust, premium feel
- **Gold**: Achievement, special rewards

### Animation Guidelines
- Card flip: 0.6s with easing
- Match celebration: 0.6s bounce
- Wrong match: 0.5s shake
- Screen transitions: 0.3s fade

## 📄 License

MIT - Free to use and modify for your Braze campaigns!

---

Need help? Check the main [Braze Games Library](https://github.com/VincentSolconBraze/braze-games-library) documentation!