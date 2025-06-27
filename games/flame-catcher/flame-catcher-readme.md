# 🔥 Flame Catcher - Braze In-App Game

> An exciting dropper-style game where players control Braze's flame mascot to catch falling rewards while avoiding bombs, optimized for Braze in-app messages.

![Flame Catcher Preview](https://cdn.braze.eu/appboy/communication/assets/image_assets/images/685d38dc0a367c00950cd7e8/original.png?1750939867)

## ✨ Features

- 🔥 **Official Braze Mascot** - Features the iconic Braze flame character
- 🎯 **5 Item Types** - Coins, stars, gems, hearts, and bombs to avoid
- 📈 **Progressive Difficulty** - Speed increases over time with multiple simultaneous items
- ❤️ **Lives System** - 5 lives, lose one for each missed reward
- 🏆 **High Score Tracking** - Persistent high scores via user attributes
- 📱 **Fully Responsive** - Works perfectly on all devices and orientations
- ♿ **Accessible** - Keyboard navigation and screen reader support
- 📊 **Complete Analytics** - Tracks every interaction and game event
- 🚀 **Lightweight** - Only ~25KB total size
- 🔌 **No Dependencies** - Pure HTML/CSS/JavaScript

## 🚀 Quick Start

1. Copy the content of `flame-catcher-index.html`
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
    --primary-color: #FF6B35;      /* Main brand color */
    --secondary-color: #F7931E;    /* Secondary color */
    --accent-color: #A333C8;       /* Accent for special elements */
    --success-color: #21BA45;      /* Success/reward color */
    --danger-color: #DB2828;       /* Danger/bomb color */
}
```

### Rewards Configuration

Modify the `rewards` array in the config:

```javascript
const config = {
    rewards: [
        { emoji: '🪙', points: 10, weight: 40, name: 'coin' },
        { emoji: '⭐', points: 20, weight: 30, name: 'star' },
        { emoji: '💎', points: 30, weight: 20, name: 'gem' },
        { emoji: '❤️', points: 50, weight: 5, name: 'heart' },
        { emoji: '💣', points: -25, weight: 15, name: 'bomb', isPenalty: true }
    ]
};
```

### Difficulty Settings

Adjust the difficulty progression:

```javascript
difficulties: [
    { time: 0, dropSpeed: 1200, fallSpeed: 2 },
    { time: 8000, dropSpeed: 900, fallSpeed: 1.8, simultaneous: 2 },
    { time: 15000, dropSpeed: 700, fallSpeed: 1.5, simultaneous: 2 },
    { time: 25000, dropSpeed: 500, fallSpeed: 1.2, simultaneous: 3 }
]
```

### Reward Tiers

Set different rewards based on score:

```javascript
rewardTiers: [
    { minScore: 1000, reward: '30% OFF', code: 'MASTER30' },
    { minScore: 500, reward: '25% OFF', code: 'GREAT25' },
    { minScore: 250, reward: '20% OFF', code: 'GOOD20' },
    { minScore: 0, reward: '15% OFF', code: 'PLAY15' }
]
```

### Text Content

Update these elements in the HTML:

```html
<h1 class="game-title">🔥 Flame Catcher</h1>
<p class="game-subtitle">Catch rewards and boost your score!</p>
<button class="start-button">PLAY NOW!</button>
```

## 📊 Analytics Events

The game automatically tracks:

| Event | When Triggered | Data Included |
|-------|----------------|---------------|
| `flame_catcher_opened` | Game loads | session_id, timestamp |
| `flame_catcher_started` | User starts playing | high_score, session_id |
| `flame_catcher_completed` | Game ends | final_score, play_duration, items_collected, lives_lost, game_over_reason |
| `flame_catcher_reward_claimed` | Reward claimed | score, reward_tier, reward_code, session_id |
| `flame_catcher_closed` | Game closes | session_duration, final_score |

### Click Tracking

- `start_game` - Start button
- `collect_coin` - Collected a coin
- `collect_star` - Collected a star
- `collect_gem` - Collected a gem
- `collect_heart` - Collected a heart
- `collect_bomb` - Hit a bomb
- `play_again` - Play again button
- `claim_reward` - Claim reward button
- `close_button` - Close game

### User Attributes Updated

- `flame_catcher_high_score` - Player's best score ever
- `flame_catcher_last_played` - Timestamp of last game played

## 🛠️ Advanced Options

### Change Game Duration

```javascript
gameDuration: 45000, // 45 seconds instead of 60
```

### Add Power-ups

```javascript
// Add to rewards array
{ emoji: '🚀', points: 0, weight: 5, name: 'rocket', isPowerUp: true }

// Handle in collectItem()
if (reward.isPowerUp) {
    activatePowerUp(reward.name);
}
```

### Add Sound Effects

```javascript
// Add sound objects
const sounds = {
    collect: new Audio('data:audio/wav;base64,...'),
    bomb: new Audio('data:audio/wav;base64,...'),
    gameOver: new Audio('data:audio/wav;base64,...')
};

// Play on collection
sounds.collect.play();
```

### Limited Plays Per Day

```javascript
// Check daily limit
const lastPlayed = brazeBridge.getUser().getCustomUserAttribute("flame_catcher_last_played");
const playsToday = brazeBridge.getUser().getCustomUserAttribute("flame_catcher_plays_today") || 0;

if (playsToday >= 3) {
    showMessage("Come back tomorrow for more plays!");
    return;
}
```

## 🎯 Use Cases

### E-commerce
- **Flash Sales**: Catch discount codes before they expire
- **Product Launch**: Collect new product emojis for exclusive access
- **Cart Abandonment**: Win back customers with instant rewards
- **VIP Programs**: Higher tier = better reward drops

### Gaming/Apps
- **Daily Rewards**: Different items each day
- **Tutorial Completion**: Teach game mechanics
- **Achievement Unlocks**: Special items for milestones
- **Currency Collection**: Gather in-game coins

### Restaurants/Food
- **Happy Hour**: Catch drink discounts
- **New Menu Items**: Collect ingredients for rewards
- **Loyalty Points**: Convert catches to points
- **Seasonal Specials**: Holiday-themed items

### B2B/SaaS
- **Feature Discovery**: Catch features to unlock
- **Onboarding Progress**: Rewards for completion
- **Upgrade Incentives**: Premium features as rare drops
- **Referral Programs**: Share to unlock better items

## 🐛 Troubleshooting

### Game doesn't display
- Check SDK version requirements (Web 2.5.0+, iOS 4.2.0+, Android 8.0.0+)
- Verify `allowUserSuppliedJavascript: true` in Web SDK
- Ensure "HTML Upload with Preview" is selected
- Test on physical devices, not just preview

### Controls not working
- Check touch event handling on mobile
- Verify no CSS conflicts with your app
- Test keyboard navigation
- Ensure collector element is properly positioned

### Analytics not tracking
- Confirm `brazeBridge` is available
- Wait for "ab.BridgeReady" event
- Check event names match your dashboard setup
- Verify `requestImmediateDataFlush()` is called

### Performance issues
- Reduce simultaneous items on older devices
- Simplify particle effects
- Test on target device types
- Monitor memory usage in long sessions

### Items falling too fast/slow
- Adjust `fallSpeed` in difficulty settings
- Test on different screen sizes
- Consider device performance
- Add dynamic difficulty adjustment

## 📱 Browser Support

- ✅ Chrome/Edge 80+
- ✅ Safari 13+
- ✅ Firefox 75+
- ✅ iOS Safari 13+
- ✅ Chrome Android 80+

## 🎮 Game Mechanics

### Scoring System
- **Coins**: 10 points (40% drop rate)
- **Stars**: 20 points (30% drop rate)
- **Gems**: 30 points (20% drop rate)
- **Hearts**: 50 points (5% drop rate)
- **Bombs**: -25 points (15% drop rate)

### Difficulty Progression
1. **0-8s**: Normal speed, single items
2. **8-15s**: Faster drops, 2 simultaneous items
3. **15-25s**: Very fast, 2 simultaneous items
4. **25-60s**: Maximum speed, 3 simultaneous items

### Lives System
- Start with 5 lives
- Lose 1 life for each missed reward (not bombs)
- Game ends when lives reach 0
- Bombs don't affect lives, only score

## 💡 Best Practices

### Performance
- Test on low-end devices
- Monitor frame rates during gameplay
- Optimize for 3G connections
- Keep total size under 50KB

### Engagement
- Start easier to hook players
- Show progress clearly
- Celebrate small wins
- Make rewards meaningful

### Accessibility
- High contrast between items
- Clear visual feedback
- Support keyboard navigation
- Test with screen readers

## 🎨 Design Tips

### Visual Hierarchy
1. Score and lives most prominent
2. Collector easily visible
3. Items clearly distinguishable
4. Background doesn't distract

### Animation Guidelines
- Item fall: Linear movement
- Collector: Smooth transitions (0.08s)
- Sparkles: 0.8s fade out
- Screen flash: 0.2s for bombs

### Mobile Considerations
- Large touch targets (60x80px collector)
- Clear item sizes (40x40px minimum)
- Responsive text sizing
- Landscape orientation support

## 📄 License

MIT - Free to use and modify for your Braze campaigns!

---

Need help? Check the main [Braze Games Library](https://github.com/VincentSolconBraze/braze-games-library) documentation or open an issue!