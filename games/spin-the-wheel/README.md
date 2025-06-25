# 🎯 Spin the Wheel - Braze In-App Game

> An interactive fortune wheel game with customizable prizes and instant rewards, optimized for Braze in-app messages.

![Preview](./preview.png)

## ✨ Features

- 🎨 **8 Customizable Segments** - Easy to modify prizes and colors
- 🎊 **Smooth Animations** - CSS3 powered wheel rotation with confetti
- 📱 **Fully Responsive** - Works perfectly on all devices
- ♿ **Accessible** - Keyboard navigation and screen reader support
- 📊 **Complete Analytics** - Tracks every user interaction
- 🚀 **Lightweight** - Only ~15KB total size
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
    --primary-color: #FF6B35;     /* Main brand color */
    --secondary-color: #F7931E;   /* Secondary color */
    --accent-color: #FCEE21;      /* Accent for effects */
    --dark-color: #2C3E50;        /* Dark text */
    --light-color: #FFFFFF;       /* Light backgrounds */
}
```

### Rewards

Modify the `rewards` array in the JavaScript:

```javascript
const rewards = [
    { 
        text: "20% OFF",           // Text on wheel
        emoji: "🎯",              // Result emoji
        code: "SAVE20",           // Promo code
        message: "Save 20%...",   // Win message
        color: "#FF6B35"          // Segment color
    },
    // Add more rewards...
];
```

### Text Content

Update these elements in the HTML:

```html
<h1>Spin & Win!</h1>              <!-- Main title -->
<p>Try your luck...</p>           <!-- Subtitle -->
<button>SPIN TO WIN!</button>     <!-- Button text -->
```

## 📊 Analytics Events

The game automatically tracks:

| Event | When Triggered | Data Included |
|-------|----------------|---------------|
| `spin_wheel_game_opened` | Game loads | timestamp |
| `wheel_spin_started` | User clicks spin | spin_count |
| `wheel_spin_completed` | Spin animation ends | reward_won, reward_code |
| `reward_displayed` | Result modal shows | reward_type, reward_code |
| `reward_claimed` | User claims reward | total_spins, game_duration |
| `play_again_clicked` | User plays again | after_spin_count |
| `game_closed` | Game closes | total_duration, last_action |

### User Attributes Updated

- `last_spin_reward` - Most recent reward code
- `total_spins` - Lifetime spin count

## 🛠️ Advanced Options

### Limit Spins Per Session

```javascript
const MAX_SPINS = 3;
if (spinCount >= MAX_SPINS) {
    spinBtn.disabled = true;
    spinBtn.textContent = "No more spins!";
}
```

### Add Weighted Probabilities

```javascript
// Add weight property to rewards
const rewards = [
    { text: "10% OFF", weight: 40, ... },  // 40% chance
    { text: "50% OFF", weight: 5, ... },   // 5% chance
];

// Implement weighted selection
function getWeightedRandom() {
    // Implementation here
}
```

### Add Timer/Urgency

```javascript
// Auto-close after 5 minutes
setTimeout(() => {
    brazeBridge.logCustomEvent("game_timeout");
    closeGame();
}, 300000);
```

## 🎯 Use Cases

### E-commerce
- Welcome offers for new users
- Win-back campaigns for inactive users
- Flash sale promotions
- Cart abandonment incentives

### Gaming/Apps
- Daily login rewards
- Level completion bonuses
- Premium upgrade incentives
- Virtual currency giveaways

### Restaurants/Food
- First-time visitor discounts
- Loyalty program bonuses
- Limited-time menu promotions
- Birthday specials

## 🐛 Troubleshooting

### Game doesn't display
- Check SDK version requirements
- Verify `allowUserSuppliedJavascript: true` in Web SDK
- Ensure "HTML Upload with Preview" is selected

### Analytics not tracking
- Confirm `brazeBridge` is available
- Check browser console for errors
- Verify event names match your setup

### Performance issues
- Reduce confetti count
- Simplify animations
- Test on target devices

## 📱 Browser Support

- ✅ Chrome/Edge 80+
- ✅ Safari 13+
- ✅ Firefox 75+
- ✅ iOS Safari 13+
- ✅ Chrome Android 80+

## 📄 License

MIT - Free to use and modify for your Braze campaigns!

---

Need help? Check the main [Braze Games Library](https://github.com/VincentSolconBraze/braze-games-library) documentation.