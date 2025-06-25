# 🎮 Braze Games Library

> A collection of interactive HTML5 games optimized for Braze in-app messages. Ready-to-use, customizable, and fully tracked!

## 🌟 Features

- ✅ **100% Braze Compatible** - Works with HTML Upload with Preview
- 📱 **Responsive Design** - Perfect on mobile and desktop
- 📊 **Full Analytics** - Complete event tracking via brazeBridge
- 🎨 **Easily Customizable** - Simple CSS variables and configuration
- ♿ **Accessible** - WCAG 2.1 AA compliant
- ⚡ **Lightweight** - Each game < 50KB
- 🔌 **No Dependencies** - Pure HTML/CSS/JS

## 🎯 Available Games

### 1. [Spin the Wheel](./games/spin-the-wheel/)
A fortune wheel game with customizable prizes and instant rewards.
- 🎰 8 customizable segments
- 🎁 Instant win rewards
- 🎊 Confetti animations
- 📊 Complete tracking

### 2. Scratch Card (Coming Soon)
### 3. Memory Game (Coming Soon)
### 4. Slot Machine (Coming Soon)
### 5. Hit the Target (Coming Soon)

## 🚀 Quick Start

### Prerequisites

**Minimum SDK Versions:**
- Web SDK: v2.5.0+ (with `allowUserSuppliedJavascript: true`)
- Android SDK: v8.0.0+
- iOS SDK: v4.2.0+ / Swift SDK: v5.4.0+

### Installation

1. **Choose a game** from the `games/` directory
2. **Copy the HTML file** content
3. **In Braze Dashboard:**
   - Create new In-App Message
   - Select "Custom Code"
   - Choose "HTML Upload with Preview"
   - Paste the game code
   - Customize as needed
   - Test & Launch! 🚀

## 📊 Analytics & Tracking

All games include comprehensive tracking:

```javascript
// Automatic events tracked:
- game_opened
- game_started
- user_action (with details)
- reward_earned
- game_completed
- game_closed
```

## 🎨 Customization

Each game uses CSS variables for easy theming:

```css
:root {
  --primary-color: #FF6B35;
  --secondary-color: #F7931E;
  --font-family: 'Arial', sans-serif;
  /* ... more variables */
}
```

## 📋 Game Development Guidelines

### Required Features
- ✅ brazeBridge integration
- ✅ Responsive design (mobile-first)
- ✅ Accessibility (keyboard nav, ARIA labels)
- ✅ Performance < 50KB total
- ✅ Offline support via Media Library
- ✅ Cross-platform compatibility

### Code Standards
- Pure vanilla JavaScript (ES6+)
- No external dependencies
- Semantic HTML5
- CSS3 with variables
- Comprehensive error handling

## 🤝 Contributing

Want to add a new game? Check our [Contributing Guide](./CONTRIBUTING.md)!

1. Fork the repository
2. Create your game in `games/your-game-name/`
3. Follow the standards above
4. Submit a Pull Request

## 📄 License

MIT License - feel free to use in your Braze campaigns!

## 🙏 Credits

Developed for the Braze community by [@VincentSolconBraze](https://github.com/VincentSolconBraze)

---

⭐ **Star this repo** if you find it helpful!