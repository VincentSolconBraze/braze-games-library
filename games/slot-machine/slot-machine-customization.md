# 🎰 Customization Guide - Slot Machine for Braze

## 📊 Game Overview

The **Slot Machine** is an engaging game of chance that creates excitement and drives conversions through instant rewards. Perfect for:
- 🛒 Boosting sales conversions (promo codes)
- 📧 Email list growth (win incentives)
- 🔄 Improving retention (regular rewards)
- 📈 Increasing engagement (gamification)

## 🎨 Visual Customization

### 1. **Brand Colors**
Modify the CSS variables at the beginning of the code:

```css
:root {
    --primary-color: #FFD700;      /* Main gold color */
    --secondary-color: #FF6B6B;    /* Secondary red */
    --accent-color: #4ECDC4;       /* Accent teal */
    --dark-color: #1A1A2E;         /* Dark background */
    --light-color: #FFFFFF;        /* Light elements */
    --reel-bg: #0F0F1E;           /* Reel background */
    --win-color: #00FF00;         /* Win indicator */
    --lose-color: #FF6B6B;        /* Loss indicator */
}
```

### 2. **Reel Styling**
Customize the slot machine appearance:

```css
.slot-machine {
    background: var(--reel-bg);
    border: 3px solid var(--primary-color);
    box-shadow: 0 0 30px rgba(255, 215, 0, 0.3);
}

.reel {
    background: rgba(255, 255, 255, 0.05);
    border: 2px solid var(--primary-color);
}
```

### 3. **Text and Messages**
Modify directly in the HTML:

```html
<h1 class="game-title">Lucky Slots</h1>              <!-- Main title -->
<p class="game-subtitle">Spin to win amazing rewards!</p>  <!-- Subtitle -->
<button>SPIN TO WIN!</button>                         <!-- Button text -->
```

## 🎁 Reward Configuration

### Reward Structure
Each reward in the JavaScript array contains:

```javascript
{
    symbol: '💎',              // Symbol on reels
    name: 'Diamond',           // Internal name
    reward: 'FREE SHIPPING',   // Display reward
    code: 'SHIPFREE',         // Promo code
    message: 'Brilliant! Free shipping on any order!'  // Win message
}
```

### Industry-Specific Examples

#### 🛍️ **E-commerce**
```javascript
{ symbol: '🍒', reward: '20% OFF', code: 'SAVE20', message: '20% off your entire cart!' },
{ symbol: '💎', reward: 'FREE SHIP', code: 'SHIP0', message: 'Free shipping, no minimum!' },
{ symbol: '⭐', reward: 'BOGO DEAL', code: 'BOGO50', message: 'Buy one, get one 50% off!' }
```

#### 🍔 **Restaurant/Food Delivery**
```javascript
{ symbol: '🍒', reward: 'FREE SIDE', code: 'FREESIDE', message: 'Free side with any entrée!' },
{ symbol: '🍇', reward: '25% OFF', code: 'FEAST25', message: '25% off your next order!' },
{ symbol: '⭐', reward: 'FREE MEAL', code: 'FREEMEAL', message: 'Your next meal is on us!' }
```

#### 🎮 **Gaming/Apps**
```javascript
{ symbol: '💎', reward: '1000 GEMS', code: 'GEMS1K', message: '1000 gems added to your account!' },
{ symbol: '⭐', reward: 'VIP 30 DAYS', code: 'VIP30', message: '30 days of VIP access unlocked!' },
{ symbol: '🍒', reward: 'RARE SKIN', code: 'SKIN01', message: 'Exclusive skin unlocked!' }
```

#### 💼 **SaaS/B2B**
```javascript
{ symbol: '🍋', reward: '1 MONTH FREE', code: 'MONTH1', message: 'Get 1 month free on any plan!' },
{ symbol: '💎', reward: '50% OFF', code: 'HALF50', message: '50% off your first 3 months!' },
{ symbol: '⭐', reward: 'PREMIUM TRIAL', code: 'PREM30', message: '30-day premium trial unlocked!' }
```

## 📈 Metrics and Analytics

### Automatically Tracked Events:

| Event | Description | Data Collected |
|-------|-------------|----------------|
| `slot_machine_opened` | Game launch | timestamp |
| `slot_spin_started` | Spin initiated | spin_count |
| `slot_spin_completed` | Spin finished | combination, is_win |
| `slot_machine_win` | Win detected | reward_type, reward_code, winning_symbol |
| `slot_machine_loss` | No win | combination |
| `slot_reward_claimed` | Reward claimed | total_spins, session_duration |
| `slot_play_again_clicked` | Continue playing | after_spin_count |
| `slot_machine_backgrounded` | Tab switched | total_spins |
| `slot_machine_closed` | Game exit | total_duration, had_win, last_action |

### User Attributes Updated:
- `last_slot_reward`: Latest reward code won
- `total_slot_spins`: Cumulative spin count
- `slot_rewards_claimed`: Total rewards claimed (incremented)

## 🔧 Advanced Options

### 1. **Session Spin Limits**
Control the number of allowed spins:

```javascript
const config = {
    maxSpinsPerSession: 3  // Default is 3, can be 1-10
};
```

### 2. **Custom Win Patterns** (Advanced)
Add specific winning combinations:

```javascript
// Check for specific patterns
if (slotResults[0] === '🍒' && slotResults[1] === '🍒') {
    // Two cherries = small win
    handlePartialWin();
}
```

### 3. **Progressive Difficulty**
Reduce win chances after each win:

```javascript
let winCount = 0;
function adjustDifficulty() {
    if (winCount > 0) {
        // Make wins 10% less likely per previous win
        const adjustment = 1 - (winCount * 0.1);
        // Apply to random generation
    }
}
```

### 4. **Time-Limited Rewards**
Add expiration to rewards:

```javascript
message: 'You won 30% off! Expires in 24 hours!'

// In claim function
brazeBridge.getUser().setCustomUserAttribute("reward_expiry", 
    new Date(Date.now() + 24*60*60*1000).toISOString()
);
```

## 📱 Mobile Optimization

The game auto-adapts but you can fine-tune:

```css
@media (max-width: 480px) {
    .reel {
        width: 75px;   /* Smaller on mobile */
        height: 100px;
    }
    .symbol {
        font-size: 3em; /* Adjust emoji size */
    }
}
```

## ⚡ Performance Optimization

### File Size
- HTML + CSS + JS: ~16KB
- Braze limit: 200KB
- Available for assets: ~184KB

### Performance Tips
1. **Reduce confetti**: Lower particle count for older devices
2. **Simplify animations**: Use fewer keyframes
3. **Optimize symbols**: Use emoji instead of images
4. **Minify code**: Use online minifiers before deployment

## 🚀 Braze Deployment

### 1. **Campaign Setup**
- Type: In-App Message
- Message Type: Custom Code
- Custom Type: HTML Upload with Preview

### 2. **Targeting Examples**
Recommended segments:
- New users (registered < 30 days)
- High-value customers (LTV > $100)
- Inactive users (no purchase > 60 days)
- Cart abandoners
- Birthday month users

### 3. **Trigger Recommendations**
- Session start (limit 1x per day)
- After adding to cart
- On specific page visit
- Custom event (e.g., `level_completed`)
- Time-based (e.g., 3 days after install)

## 💡 Best Practices

### ✅ **DO**
- Test on real devices (iOS & Android)
- Limit to 3-5 spins maximum
- Offer real, valuable rewards
- Track conversion rates
- A/B test different rewards
- Use clear expiration dates
- Include terms & conditions

### ❌ **DON'T**
- Allow unlimited spins
- Promise unrealistic rewards
- Show too frequently (max 1x/week)
- Forget mobile users
- Neglect loading states
- Use copyrighted symbols
- Make claims about odds

## 🎯 KPI Examples

| Metric | Target | Calculation |
|--------|--------|-------------|
| Engagement Rate | > 60% | spins / opens |
| Win Rate | 30-40% | wins / total spins |
| Claim Rate | > 80% | claims / wins |
| Conversion Rate | > 25% | purchases / claims |
| Avg Session Time | 45-90s | mean session duration |
| Replay Rate | > 40% | play_again / eligible_users |

## 🛠️ Troubleshooting

### "Reels won't spin"
- Check JavaScript console for errors
- Verify CSS animations are supported
- Test transition timing
- Ensure buttons aren't disabled

### "Rewards don't show"
- Verify reward configuration matches symbols
- Check CSS display properties
- Test in Braze preview mode
- Confirm win detection logic

### "Poor performance"
- Reduce confetti count (line 440)
- Simplify reel animations
- Remove box-shadows on mobile
- Test on minimum spec devices

### "Analytics missing"
- Confirm SDK version compatibility
- Check for brazeBridge availability
- Verify event names match dashboard
- Call requestImmediateDataFlush()

## 📞 Support

For implementation help:
1. Check Braze docs: [HTML In-App Messages](https://www.braze.com/docs)
2. Test in Braze Preview
3. Use browser DevTools
4. Check JavaScript console

## 🏆 Success Tips

### Week 1: Soft Launch
- Target 10% of users
- High-value rewards
- Monitor engagement

### Week 2: Optimize
- A/B test rewards
- Adjust spin limits
- Refine targeting

### Week 3: Scale
- Expand to 50% users
- Add seasonal themes
- Create urgency

### Week 4: Analyze
- Review conversion lift
- Calculate ROI
- Plan next iteration

---

**💪 Pro Tip**: Start with generous rewards (20-30% off) to build excitement, then optimize based on your margins and conversion data!