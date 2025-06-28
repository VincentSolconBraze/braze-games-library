# 🎯 Spin the Wheel - Braze In-App Game

> An interactive fortune wheel game with standardized Braze tracking, tier-based rewards, and complete analytics integration. Fully compliant with Braze HTML In-App Message standards.

![Preview](https://cdn.braze.eu/appboy/communication/assets/image_assets/images/685cf591b1c74f0065bcdb09/original.png?1750922641)

## ✨ Features

- 🎨 **8 Customizable Segments** - Easy to modify prizes and colors
- 🏆 **Tier-Based Rewards** - Bronze, Silver, Gold, and Platinum levels
- 📊 **Standardized Analytics** - Complete Braze event tracking with nested objects
- 🎊 **Smooth Animations** - CSS3 powered wheel rotation with confetti
- 📱 **Fully Responsive** - Works perfectly on all devices
- ♿ **Accessible** - WCAG compliant with keyboard navigation and screen reader support
- 🚀 **Performance Optimized** - Memory management and cleanup
- 🔒 **Error Tracking** - Comprehensive error handling and reporting
- 🎯 **Braze Compliant** - Follows all Braze HTML In-App Message standards

## 📋 Requirements

### Minimum SDK Versions
- **Web SDK**: v2.5.0+ (with `allowUserSuppliedJavascript: true`)
- **Android SDK**: v8.0.0+
- **iOS SDK**: v4.2.0+ / Swift SDK: v5.4.0+

### Message Type
- **Required**: "HTML Upload with Preview" type only
- **Size**: < 25KB compressed (< 200KB uncompressed)

## 🚀 Quick Start

1. Copy the content of `index.html`
2. In Braze Dashboard:
   - Create new In-App Message
   - Select **Custom Code**
   - Choose **HTML Upload with Preview**
   - Paste the code
3. Test in preview mode
4. Launch your campaign!

## 📊 Standardized Event Tracking

This game implements the Braze standardized event schema with nested object properties:

### Events Tracked

| Event Name | When Triggered | Properties Structure |
|------------|----------------|---------------------|
| `game_opened` | Game loads | `game`, `context` |
| `game_started` | First spin | `game`, `context`, `performance` |
| `game_action` | Any button click | `game`, `context`, `action` |
| `game_completed` | Spin completes | `game`, `context`, `performance`, `reward_info` |
| `reward_earned` | Reward calculated | `game`, `context`, `reward` |
| `reward_claimed` | User claims code | `game`, `context`, `reward`, `performance` |
| `game_closed` | Game closes | `game`, `context`, `performance` |
| `game_error` | Any error occurs | `game`, `context`, `error` |

### Event Properties Schema

```javascript
{
  game: {
    type: "spin_wheel",        // Game identifier
    session_id: "unique_id",   // Unique session ID
    version: "1.0.0"          // Game version
  },
  performance: {
    score: Number,             // Value-based score
    duration_seconds: Number,  // Time played
    actions_taken: Number,     // Total spins
    efficiency_percent: Number,// 0-100 performance
    completion_status: String  // completed/abandoned
  },
  context: {
    device_type: String,       // mobile/desktop
    is_replay: Boolean,        // First play or replay
    timestamp: Number          // Event timestamp
  }
}
```

### User Attributes Updated

- `last_spin_reward_code` - Most recent reward code
- `last_spin_reward_tier` - Tier achieved (bronze/silver/gold/platinum)
- `total_spins_lifetime` - Total spins across all sessions
- `last_game_played` - Set to "spin_wheel"

## 🎨 Customization

### 1. Braze Brand Colors (Required)

The game uses Braze's official brand colors by default:

```css
:root {
    /* Braze Brand Colors (NON MODIFIABLE) */
    --braze-orange: #FFA524;
    --braze-pink: #FFA4FB;
    --braze-purple: #801ED7;
    
    /* Map to game colors */
    --game-primary: var(--braze-orange);
    --game-secondary: var(--braze-pink);
    --game-accent: var(--braze-purple);
}
```

### 2. Wheel Segments

Modify the `rewards` array to customize prizes:

```javascript
const rewards = [
    { 
        text: "20% OFF",     // Display text
        value: 85,           // Performance value (0-100)
        color: "#FF6B35"     // Segment color
    },
    // Add up to 8 segments
];
```

### 3. Reward Tiers

The game automatically assigns tiers based on segment value:

| Tier | Value Range | Reward Prefix | Color |
|------|-------------|---------------|-------|
| Bronze | 0-33 | B | #CD7F32 |
| Silver | 34-66 | S | #C0C0C0 |
| Gold | 67-89 | G | #FFD700 |
| Platinum | 90-100 | P | #E5E4E2 |

### 4. Text Content

Update these elements in the HTML:

```html
<h1>Spin & Win!</h1>              <!-- Main title -->
<p>Try your luck...</p>           <!-- Subtitle -->
<button>SPIN TO WIN!</button>     <!-- Button text -->
```

## 🏆 Reward System

### Code Generation Pattern

Reward codes follow this pattern: `[TIER][GAME][SCORE][TIME]`

Example: `GSPI85A3K7`
- `G` = Gold tier
- `SPI` = First 3 letters of "spin_wheel"
- `85` = Score value
- `A3K7` = Timestamp hash

### Tier Messages

Each tier has a unique congratulatory message:
- **Bronze**: "Good job! You've earned a bronze reward!"
- **Silver**: "Great spin! You've won a silver prize!"
- **Gold**: "Amazing! You've hit the gold jackpot!"
- **Platinum**: "INCREDIBLE! You've achieved platinum status!"

## 🛠️ Advanced Configuration

### Performance Monitoring

The game includes built-in performance monitoring:

```javascript
const GAME_CONFIG = {
    type: "spin_wheel",
    version: "1.0.0",
    braze_category: "reward",
    max_session_duration: 120,    // Max seconds
    target_completion_time: 60    // Target seconds
};
```

### Memory Management

Automatic cleanup of resources:

```javascript
// All timeouts and intervals are tracked
memoryManager.addTimeout(callback, delay);

// Cleanup on game close
memoryManager.cleanup();
```

### Error Handling

Comprehensive error tracking:

```javascript
window.addEventListener('error', function(e) {
    gameTracker?.trackEvent('game_error', {
        error: {
            message: e.message,
            filename: e.filename,
            line: e.lineno,
            type: 'javascript_error'
        }
    });
});
```

## 🎯 Use Cases

### E-commerce
- **New User Welcome**: 100% win rate for first-time visitors
- **Cart Abandonment**: High-value segments for recovery
- **VIP Rewards**: Platinum tier for loyal customers
- **Flash Sales**: Time-limited spin opportunities

### Gaming/Apps
- **Daily Rewards**: Reset spin count daily
- **Level Completion**: Unlock better reward tiers
- **Achievement Bonuses**: Special segments for milestones
- **Virtual Currency**: Award in-game credits

### Restaurants/Food
- **First Visit**: Guaranteed discount codes
- **Birthday Specials**: Exclusive birthday tier
- **Loyalty Points**: Convert spins to points
- **Menu Promotions**: Feature new items as prizes

## 🐛 Troubleshooting

### Game doesn't display
- ✓ Check SDK version requirements
- ✓ Verify `allowUserSuppliedJavascript: true` in Web SDK
- ✓ Ensure "HTML Upload with Preview" is selected
- ✓ Test in Braze preview mode first

### Events not tracking
- ✓ Confirm `brazeBridge` is available
- ✓ Check browser console for errors
- ✓ Verify event names in your analytics
- ✓ Ensure `requestImmediateDataFlush()` is called

### Performance issues
- ✓ Reduce confetti count (line 50 in createConfetti)
- ✓ Simplify animations for older devices
- ✓ Check total file size (< 200KB)
- ✓ Test on minimum SDK versions

### Reward codes not generating
- ✓ Check segment value property (0-100)
- ✓ Verify reward system initialization
- ✓ Test tier calculation logic
- ✓ Confirm user attribute updates

## 📱 Browser Support

- ✅ Chrome/Edge 80+
- ✅ Safari 13+
- ✅ Firefox 75+
- ✅ iOS Safari 13+
- ✅ Chrome Android 80+

## 🔄 Migration from Previous Version

If updating from the older version:

1. **Event Names**: Update any campaigns using old event names
   - Old: `spin_wheel_game_opened` → New: `game_opened`
   - Old: `wheel_spin_started` → New: `game_started`
   - Old: `wheel_spin_completed` → New: `game_completed`

2. **Event Properties**: Update segments using flat properties
   - Old: `reward_won`, `spin_count`
   - New: Nested structure with `game`, `performance`, `context`

3. **User Attributes**: New attributes added
   - Added: `last_spin_reward_tier`
   - Added: `last_game_played`

## 📄 License

MIT - Free to use and modify for your Braze campaigns!

---

Need help? Check the main [Braze Games Library](https://github.com/VincentSolconBraze/braze-games-library) documentation.