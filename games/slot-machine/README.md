# 🎰 Slot Machine - Braze In-App Game (v2.0 Compliant)

> A performance-based slot machine game with dynamic tiered rewards and comprehensive analytics, fully compliant with Braze v2.0 standards.

![Preview](https://cdn.braze.eu/appboy/communication/assets/image_assets/images/685cf4bcd4422900659cbf91/original.png?1750922428)

## ✨ Features

- 🎰 **3-Reel Classic Slot Machine** - Authentic casino-style gameplay
- 🏆 **Dynamic Tier System** - Bronze/Silver/Gold/Platinum rewards based on performance
- 🎯 **6 Weighted Symbols** - Point-based system for fair rewards
- 📊 **Standardized Analytics** - Nested event structure with performance metrics
- 🎊 **Smooth Animations** - Hardware-accelerated reel spinning
- 📱 **Fully Responsive** - Optimized for all devices
- ♿ **Accessible** - WCAG 2.1 compliant with screen reader support
- 🧹 **Memory Managed** - Automatic cleanup prevents leaks
- 🚀 **Lightweight** - ~30KB total (well under 200KB limit)
- 🔌 **No Dependencies** - Pure HTML/CSS/JavaScript

## 🆕 v2.0 Compliance Features

- ✅ **BrazeGameTracker** class for standardized event handling
- ✅ **BrazeRewardSystem** for dynamic tier-based rewards
- ✅ **GameMemoryManager** for resource cleanup
- ✅ **Nested event structure** with game/performance/context
- ✅ **Braze brand colors** as CSS constants
- ✅ **Performance metrics** tracking (score, efficiency, duration)
- ✅ **Error handling** with event tracking
- ✅ **Standardized event names** (game_opened, game_started, etc.)

## 🚀 Quick Start

1. Copy the content of `slot-machine-index.html`
2. In Braze Dashboard:
   - Create new In-App Message
   - Select "Custom Code"
   - Choose **"HTML Upload with Preview"** (Required)
   - Paste the code
3. Verify SDK versions meet requirements
4. Test & Launch!

## 📋 SDK Requirements

| Platform | Minimum Version | Configuration |
|----------|-----------------|---------------|
| Web SDK | 2.5.0+ | `allowUserSuppliedJavascript: true` |
| Android SDK | 8.0.0+ | - |
| iOS SDK | 4.2.0+ | - |
| Swift SDK | 5.4.0+ | - |

## 🎨 Customization

### Colors (Braze Compliant)

```css
:root {
    /* Braze Brand Colors (DO NOT MODIFY) */
    --braze-orange: #FFA524;
    --braze-pink: #FFA4FB;
    --braze-purple: #801ED7;
    
    /* Map your game colors to Braze */
    --game-primary: var(--braze-orange);
    --game-secondary: var(--braze-pink);
    --game-accent: var(--braze-purple);
}
```

### Dynamic Reward Tiers

The game automatically calculates rewards based on performance:

```javascript
// Efficiency = (win_rate + symbol_value) / 2
// Bronze: 0-33% → 10% OFF
// Silver: 34-66% → 15% OFF
// Gold: 67-89% → 25% OFF
// Platinum: 90-100% → 50% OFF
```

### Symbol Configuration

```javascript
symbolPoints: {
    '🍒': 100,   // Low value
    '🍋': 150,
    '🍊': 200,
    '🍇': 300,
    '💎': 500,   // High value
    '⭐': 1000   // Jackpot
}
```

## 📊 Analytics Events (v2.0 Standard)

All events follow the standardized nested structure:

| Event Name | Trigger | Key Data |
|------------|---------|----------|
| `game_opened` | Game loads | session_id, version |
| `game_started` | First spin | device_type, difficulty |
| `game_action` | Each spin | spin_number, context |
| `reward_earned` | Win occurs | tier, code, value |
| `reward_claimed` | Claim button | reward details |
| `game_closed` | Exit/Complete | performance metrics |
| `game_error` | JS errors | error details |

### Event Structure Example

```javascript
{
    game: {
        type: "slot_machine",
        session_id: "1234567890_abc123def",
        version: "1.0.0"
    },
    performance: {
        score: 1500,
        duration_seconds: 45,
        actions_taken: 3,
        efficiency_percent: 67,
        completion_status: "completed"
    },
    context: {
        difficulty: "medium",
        device_type: "mobile",
        is_replay: false
    }
}
```

### User Attributes Updated

- `last_slot_reward` - Most recent reward code
- `last_slot_tier` - Latest tier achieved
- `total_slot_spins` - Lifetime spin count
- `slot_high_score` - Best score achieved
- `slot_rewards_claimed` - Number of rewards claimed

## 🛠️ Advanced Configuration

### Game Settings

```javascript
const GAME_CONFIG = {
    type: "slot_machine",
    version: "1.0.0",
    braze_category: "reward",
    session_id: "timestamp_randomstring"
};

const config = {
    maxSpinsPerSession: 3,      // Limit spins (1-10)
    spinDuration: 2000,         // Animation time
    reelDelay: 300,            // Sequential stops
    target_completion_time: 60  // Expected duration
};
```

### Custom Reward Values

Override default tier rewards:

```javascript
// In BrazeRewardSystem.getRewardValue()
const values = {
    bronze: 'FREE SHIPPING',
    silver: '$15 OFF',
    gold: '$25 OFF',
    platinum: '50% OFF'
};
```

## 🎯 Use Cases by Industry

### E-commerce
- **Trigger**: Cart abandonment
- **Config**: 3 spins, percentage discounts
- **Goal**: Recover lost sales

### Gaming/Apps
- **Trigger**: Level completion
- **Config**: 1 spin, virtual currency
- **Goal**: Reward engagement

### Restaurants
- **Trigger**: First app open
- **Config**: 3 spins, menu discounts
- **Goal**: Drive first order

### SaaS/B2B
- **Trigger**: Trial expiration
- **Config**: 1 spin, upgrade discounts
- **Goal**: Convert to paid

## 🐛 Troubleshooting

### Game doesn't display
- ✓ Check SDK version requirements
- ✓ Verify `allowUserSuppliedJavascript: true`
- ✓ Ensure "HTML Upload with Preview" selected
- ✓ Test brazeBridge availability

### Events not tracking
- ✓ Check for "ab.BridgeReady" event
- ✓ Verify nested event structure
- ✓ Confirm session_id format
- ✓ Review console for errors

### Wrong tier displayed
- ✓ Check efficiency calculation
- ✓ Verify symbol point values
- ✓ Test win rate logic
- ✓ Review tier boundaries

### Performance issues
- ✓ Test GameMemoryManager cleanup
- ✓ Reduce confetti particles
- ✓ Check animation frame rate
- ✓ Monitor memory usage

## 📱 Browser Support

- ✅ Chrome/Edge 80+
- ✅ Safari 13+
- ✅ Firefox 75+
- ✅ iOS Safari 13+
- ✅ Chrome Android 80+

## 🎮 Game Mechanics

### How It Works
1. User gets 3 spins per session (configurable)
2. Each reel stops independently with animation
3. Matching 3 symbols triggers win calculation
4. Performance determines reward tier
5. Dynamic code generated: `[Tier][Game][Score][Random]`
6. User can claim or play again

### Performance Calculation
```
Efficiency = (Win Rate + Symbol Value) / 2
Win Rate = (Wins / Spins) × 100
Symbol Value = (Points / Max Points) × 100
```

### Tier Distribution
- **Bronze** (0-33%): Entry rewards
- **Silver** (34-66%): Standard rewards
- **Gold** (67-89%): Premium rewards
- **Platinum** (90-100%): Top tier rewards

## 📈 Performance Benchmarks

| Metric | Target | Typical |
|--------|--------|---------|
| Load Time | < 2s | 1.2s |
| Frame Rate | 60fps | 60fps |
| Memory Usage | < 50MB | 35MB |
| Event Latency | < 100ms | 50ms |
| Session Duration | 45-90s | 65s |

## 🔒 Security & Compliance

- ✅ No external dependencies
- ✅ No localStorage/sessionStorage usage
- ✅ XSS protection via proper encoding
- ✅ WCAG 2.1 accessibility compliance
- ✅ Braze SDK security standards
- ✅ Error boundary implementation

## 📄 License

MIT - Free to use and modify for your Braze campaigns!

---

## 🤝 Contributing

See [CONTRIBUTING.md](https://github.com/VincentSolconBraze/braze-games-library/blob/main/CONTRIBUTING.md) for guidelines.

## 🙋 Need Help?

- 📧 Contact your Braze Customer Success Manager
- 📚 Review [Braze HTML In-App Messages docs](https://www.braze.com/docs)
- 🎮 Check other games in the [Braze Games Library](https://github.com/VincentSolconBraze/braze-games-library)
- 💬 Open an issue on GitHub

---

**v2.0** | Updated for Braze compliance standards | Dynamic rewards & standardized analytics
