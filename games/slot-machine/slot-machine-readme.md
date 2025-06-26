# 🎰 Slot Machine - Braze In-App Game

> An exciting slot machine game with smooth reel animations and instant rewards, optimized for Braze in-app messages.

![Preview](https://cdn.braze.eu/appboy/communication/assets/image_assets/images/685cf4bcd4422900659cbf91/original.png?1750922428)

## ✨ Features

- 🎰 **3-Reel Classic Slot Machine** - Authentic casino-style gameplay
- 🎯 **6 Different Symbols** - Fruits, diamonds, and stars
- 🎊 **Smooth Animations** - Realistic reel spinning with sequential stops
- 📱 **Fully Responsive** - Perfect on all devices
- ♿ **Accessible** - Full keyboard navigation and screen reader support
- 📊 **Complete Analytics** - Tracks every spin and reward
- 🚀 **Lightweight** - Only ~16KB total size
- 🔌 **No Dependencies** - Pure HTML/CSS/JavaScript

## 🚀 Quick Start

1. Copy the content of `index.html`
2. In Braze Dashboard:
   - Create new In-App Message
   - Select "Custom Code"
   - Choose "HTML Upload with Preview"
   - Paste the code
3. Test & Launch!

## 🎨 Customization

### Colors

Edit the CSS variables at the top of the file:

```css
:root {
    --primary-color: #FFD700;      /* Gold accents */
    --secondary-color: #FF6B6B;    /* Red highlights */
    --accent-color: #4ECDC4;       /* Teal buttons */
    --dark-color: #1A1A2E;         /* Dark background */
    --light-color: #FFFFFF;        /* Light text */
}
```

### Symbols & Rewards

Modify the `config` object in the JavaScript:

```javascript
const config = {
    symbols: ['🍒', '🍋', '🍊', '🍇', '💎', '⭐'],
    rewards: [
        { 
            symbol: '🍒',
            name: 'Cherry',
            reward: '10% OFF',
            code: 'CHERRY10',
            message: 'Sweet! You won 10% off!'
        },
        // Add more rewards...
    ]
};
```

### Text Content

Update these elements in the HTML:

```html
<h1 class="game-title">Lucky Slots</h1>        <!-- Main title -->
<p class="game-subtitle">Spin to win!</p>      <!-- Subtitle -->
<button>SPIN TO WIN!</button>                   <!-- Button text -->
```

## 📊 Analytics Events

The game automatically tracks:

| Event | When Triggered | Data Included |
|-------|----------------|---------------|
| `slot_machine_opened` | Game loads | timestamp |
| `slot_spin_started` | User clicks spin | spin_count |
| `slot_spin_completed` | Spin animation ends | combination, is_win |
| `slot_machine_win` | Matching symbols | reward_type, reward_code |
| `slot_machine_loss` | No match | combination |
| `slot_reward_claimed` | User claims reward | total_spins, session_duration |
| `slot_play_again_clicked` | Play again button | after_spin_count |
| `slot_machine_closed` | Game closes | total_duration, had_win |

### User Attributes Updated

- `last_slot_reward` - Most recent reward code won
- `total_slot_spins` - Lifetime spin count (incremented)
- `slot_rewards_claimed` - Number of rewards claimed

## 🛠️ Advanced Options

### Limit Spins Per Session

Default is 3 spins. Change in config:

```javascript
const config = {
    maxSpinsPerSession: 5  // Allow 5 spins
};
```

### Add Weighted Probabilities

```javascript
// Force specific outcomes (for testing)
function getWeightedResult() {
    const random = Math.random();
    if (random < 0.1) return 5; // 10% chance for stars
    if (random < 0.3) return 4; // 20% chance for diamonds
    // etc...
}
```

### Custom Reward Messages

```javascript
rewards: [
    {
        symbol: '💎',
        reward: 'VIP ACCESS',
        code: 'VIP2024',
        message: 'Diamond status unlocked!'
    }
]
```

### Add Sound Effects

```javascript
// Add after win detection
const winSound = new Audio('data:audio/wav;base64,...');
winSound.play();
```

## 🎯 Use Cases

### E-commerce
- Cart abandonment recovery
- First purchase incentive
- Loyalty rewards
- Seasonal promotions

### Gaming/Apps
- Daily login bonus
- Premium currency rewards
- Power-up unlocks
- Achievement celebrations

### Restaurants/Retail
- Visit incentives
- Menu item discounts
- Happy hour promotions
- Birthday rewards

### SaaS/B2B
- Trial extensions
- Feature unlocks
- Discount codes
- Upgrade incentives

## 🐛 Troubleshooting

### Game doesn't display
- Check SDK version requirements (Web 2.5.0+, Android 8.0.0+, iOS 4.2.0+)
- Verify `allowUserSuppliedJavascript: true` in Web SDK
- Ensure "HTML Upload with Preview" is selected

### Reels don't spin smoothly
- Reduce animation complexity on older devices
- Test on target devices
- Consider reducing reel symbols

### Analytics not tracking
- Confirm `brazeBridge` is available
- Check for "ab.BridgeReady" event
- Verify event names in dashboard

### Rewards not showing
- Check reward configuration
- Verify CSS classes are applied
- Test in Braze preview mode

## 📱 Browser Support

- ✅ Chrome/Edge 80+
- ✅ Safari 13+
- ✅ Firefox 75+
- ✅ iOS Safari 13+
- ✅ Chrome Android 80+

## 🎮 Game Mechanics

### How It Works
1. User gets 3 spins per session
2. Each reel stops independently
3. Matching 3 symbols = win
4. Different symbols = different rewards
5. Rewards can be claimed instantly

### Symbol Probability
Each symbol has equal chance (16.67%) by default. Can be modified for different difficulties.

### Session Limits
- 3 spins per session (configurable)
- Resets on new message view
- Tracks total lifetime spins

## 📄 License

MIT - Free to use and modify for your Braze campaigns!

---

Need help? Check the main [Braze Games Library](https://github.com/VincentSolconBraze/braze-games-library) documentation.