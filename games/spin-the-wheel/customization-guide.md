# 🎨 Spin the Wheel - Customization Guide

> A comprehensive guide for marketing teams to customize the Spin the Wheel game for their Braze campaigns.

## 🚀 Quick Customization (5 minutes)

For teams who need to launch quickly, here are the essential customizations:

### 1. Update Brand Colors

Find this section at the top of the HTML file and update the game colors to match your brand:

```css
/* Around line 10-15 */
--game-primary: var(--braze-orange);     /* Change to your primary color */
--game-secondary: var(--braze-pink);     /* Change to your secondary color */
--game-accent: var(--braze-purple);      /* Change to your accent color */
```

**Example for a blue brand:**
```css
--game-primary: #2196F3;
--game-secondary: #03A9F4;
--game-accent: #00BCD4;
```

### 2. Customize Wheel Segments

Find the `rewards` array (around line 420) and update with your prizes:

```javascript
const rewards = [
    { text: "20% OFF", value: 85, color: "#FF6B35" },
    { text: "FREE SHIP", value: 75, color: "#F7931E" },
    // ... update these with your rewards
];
```

**What each property means:**
- `text`: What shows on the wheel (keep it short!)
- `value`: Performance score (0-100) - higher = better tier
- `color`: The segment color (use hex codes)

### 3. Update Game Text

Search for these lines and update with your messaging:

```html
<!-- Around line 360 -->
<h1>Spin & Win!</h1>                           <!-- Your headline -->
<p>Try your luck and win amazing prizes!</p>   <!-- Your subheadline -->

<!-- Around line 380 -->
<button>SPIN TO WIN!</button>                  <!-- Your CTA text -->
```

## 🎯 Reward Tier System Explained

The game automatically assigns reward tiers based on the `value` property:

| If value is... | Tier | What it means | Code prefix |
|----------------|------|---------------|-------------|
| 0-33 | Bronze 🥉 | Basic reward | B |
| 34-66 | Silver 🥈 | Good reward | S |
| 67-89 | Gold 🥇 | Great reward | G |
| 90-100 | Platinum 🏆 | Best reward | P |

**Example setup for an e-commerce campaign:**
```javascript
const rewards = [
    { text: "5% OFF", value: 20, color: "#3F51B5" },      // Bronze
    { text: "10% OFF", value: 40, color: "#E91E63" },     // Silver
    { text: "15% OFF", value: 60, color: "#9C27B0" },     // Silver
    { text: "20% OFF", value: 85, color: "#FF6B35" },     // Gold
    { text: "25% OFF", value: 90, color: "#00BCD4" },     // Platinum
    { text: "FREE SHIP", value: 75, color: "#F7931E" },   // Gold
    { text: "BOGO", value: 100, color: "#8BC34A" },       // Platinum
    { text: "MYSTERY", value: 95, color: "#FCEE21" }      // Platinum
];
```

## 🎲 Probability & Fairness

By default, each segment has an **equal chance** of being selected (12.5% for 8 segments).

### Want to Control Win Rates?

You can modify the selection logic to favor certain segments:

```javascript
// Find the spinWheel function (around line 500)
// Replace this line:
const winningIndex = Math.floor(Math.random() * totalSegments);

// With weighted selection:
const winningIndex = getWeightedIndex();

// Add this function:
function getWeightedIndex() {
    // Example: 70% chance for lower-value rewards
    const rand = Math.random();
    if (rand < 0.7) {
        // Return bronze/silver tier segments (0-3)
        return Math.floor(Math.random() * 4);
    } else {
        // Return gold/platinum tier segments (4-7)
        return 4 + Math.floor(Math.random() * 4);
    }
}
```

## 🎨 Visual Customization

### Background Gradient

The game container has a purple gradient by default:

```css
/* Around line 100 */
#game-container {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
}
```

**Popular alternatives:**
```css
/* Warm sunset */
background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);

/* Cool ocean */
background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);

/* Elegant dark */
background: linear-gradient(135deg, #2D3561 0%, #C05C7E 100%);
```

### Confetti Colors

Customize the celebration confetti:

```javascript
// Around line 650
const colors = ['#FF6B35', '#F7931E', '#FCEE21', '#8BC34A', '#00BCD4', '#9C27B0'];
// Change to your brand colors
```

### Button Styles

Make the spin button match your brand:

```css
/* Around line 180 */
#spin-btn {
    background: linear-gradient(135deg, var(--game-primary), var(--game-secondary));
    /* Change gradient colors or use solid color: */
    /* background: #2196F3; */
}
```

## 📊 Analytics & Tracking

### What Gets Tracked Automatically

Every game session tracks:
- How many times users spin
- Which rewards they win
- How long they play
- If they claim or abandon rewards
- Device type (mobile/desktop)

### Custom User Attributes Set

After playing, these attributes are saved to the user profile:
- `last_spin_reward_code` - The reward code they won
- `last_spin_reward_tier` - bronze/silver/gold/platinum
- `total_spins_lifetime` - How many times they've ever spun
- `last_game_played` - Set to "spin_wheel"

### Using This Data

You can create Braze segments like:
- Users who won platinum tier rewards
- Users who spun but didn't claim
- Users who played more than 3 times
- Users who haven't played in 30 days

## 🌍 Localization

### Translating the Game

Replace all text content for different languages:

```javascript
// Add at the top of the script section
const translations = {
    en: {
        title: "Spin & Win!",
        subtitle: "Try your luck and win amazing prizes!",
        spinButton: "SPIN TO WIN!",
        spinningButton: "SPINNING...",
        congratulations: "Congratulations!",
        claimButton: "Claim Reward",
        playAgainButton: "Play Again"
    },
    es: {
        title: "¡Gira y Gana!",
        subtitle: "¡Prueba tu suerte y gana premios increíbles!",
        spinButton: "¡GIRAR PARA GANAR!",
        // ... etc
    }
};

// Use Liquid to get user language
const userLang = '{{ ${language} }}' || 'en';
const t = translations[userLang] || translations.en;
```

## 🎁 Campaign Ideas

### New User Welcome
```javascript
const rewards = [
    { text: "15% OFF", value: 70, color: "#4CAF50" },
    { text: "20% OFF", value: 85, color: "#2196F3" },
    { text: "FREE SHIP", value: 75, color: "#FF9800" },
    { text: "25% OFF", value: 90, color: "#9C27B0" },
    // All high-value to ensure good first impression
];
```

### Cart Abandonment
```javascript
const rewards = [
    { text: "5% OFF", value: 30, color: "#9E9E9E" },
    { text: "10% OFF", value: 50, color: "#03A9F4" },
    { text: "FREE SHIP", value: 75, color: "#4CAF50" },
    { text: "15% OFF", value: 80, color: "#FF5722" },
    // Mix of values to incentivize completion
];
```

### VIP/Loyalty Program
```javascript
const rewards = [
    { text: "DOUBLE PTS", value: 85, color: "#FFD700" },
    { text: "TRIPLE PTS", value: 95, color: "#E5E4E2" },
    { text: "FREE GIFT", value: 90, color: "#FF1744" },
    { text: "VIP ACCESS", value: 100, color: "#AA00FF" },
    // All high-value for VIP customers
];
```

## ⚙️ Advanced Features

### Limit Spins Per Session

Add this after the `spinCount++` line:

```javascript
// Around line 540
spinCount++;

// Add spin limit
const MAX_SPINS = 3;
if (spinCount >= MAX_SPINS) {
    spinBtn.disabled = true;
    spinBtn.textContent = "No more spins today!";
}
```

### Add Countdown Timer

Create urgency with a timer:

```javascript
// Add after initializeGame function
function startCountdown(minutes) {
    const endTime = Date.now() + (minutes * 60 * 1000);
    
    const timer = setInterval(() => {
        const remaining = endTime - Date.now();
        if (remaining <= 0) {
            clearInterval(timer);
            closeGame();
        }
        // Update UI with remaining time
        const mins = Math.floor(remaining / 60000);
        const secs = Math.floor((remaining % 60000) / 1000);
        document.querySelector('.header p').textContent = 
            `Offer expires in ${mins}:${secs.toString().padStart(2, '0')}`;
    }, 1000);
}

// Call in initializeGame
startCountdown(5); // 5 minute timer
```

### Different Rewards for User Segments

Use Liquid to customize based on user attributes:

```javascript
// Use Braze Liquid templating
const rewards = [
    {% if {{custom_attribute.${vip_status}}} == 'gold' %}
    { text: "30% OFF", value: 95, color: "#FFD700" },
    { text: "40% OFF", value: 100, color: "#E5E4E2" },
    {% else %}
    { text: "10% OFF", value: 50, color: "#2196F3" },
    { text: "15% OFF", value: 70, color: "#4CAF50" },
    {% endif %}
    // ... more segments
];
```

## 🚫 Common Mistakes to Avoid

1. **Don't use segments text that's too long** - Keep under 10 characters
2. **Don't use low contrast colors** - Text needs to be readable
3. **Don't forget to test on mobile** - Most users are on phones
4. **Don't remove the close button** - Users must be able to exit
5. **Don't modify the tracking code** - It's standardized for a reason

## 💡 Tips for Success

1. **Use contrasting colors** - Make each segment visually distinct
2. **Keep rewards realistic** - Don't offer what you can't deliver
3. **Test the experience** - Actually play the game before launching
4. **Monitor the analytics** - Check completion rates and adjust
5. **A/B test different setups** - Try different reward structures

## 🆘 Need Help?

If you encounter issues:

1. **Check the browser console** - Press F12 and look for red errors
2. **Test in Braze preview** - Use the preview mode before launching
3. **Verify SDK versions** - Ensure users have compatible app versions
4. **Simplify first** - Start with default setup, then customize

Remember: The game is designed to work out-of-the-box. Only customize what you need to change for your campaign goals.

---

For technical support, consult your Braze CSM or engineering team.