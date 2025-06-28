# 🎮 Braze Games Library

> A collection of interactive HTML5 games optimized for Braze in-app messages, featuring standardized analytics, dynamic rewards, and full v2.0 compliance.

## 🚀 What's New in v2.0

- ✅ **Standardized Event Tracking** - Nested object structure across all games
- ✅ **Dynamic Reward System** - Performance-based tier rewards (Bronze/Silver/Gold/Platinum)
- ✅ **Enhanced Analytics** - Comprehensive performance metrics
- ✅ **Memory Management** - Automatic cleanup prevents leaks
- ✅ **Braze Brand Colors** - Consistent CSS implementation
- ✅ **Error Handling** - Global error tracking for debugging

## 📋 Compliance Standards

All games in this library follow Braze v2.0 compliance standards:

- **Event Structure**: Nested objects with `game`, `performance`, and `context`
- **Event Names**: Standardized (`game_opened`, `game_started`, `game_action`, etc.)
- **CSS Variables**: Braze brand colors as non-modifiable constants
- **Performance Tracking**: Score, duration, efficiency, and completion status
- **SDK Requirements**: Web 2.5.0+, Android 8.0.0+, iOS 4.2.0+

## 🎯 Available Games

### 1. [Spin the Wheel](./games/spin-the-wheel/) ⚡
A fortune wheel game with customizable prizes and instant rewards.
- 🎰 8 customizable segments
- 🎁 Instant win rewards
- 🎊 Confetti animations
- 📊 Complete tracking
- **Category**: `reward` | **Status**: Ready

### 2. [Scratch Card](./games/scratch-card/) 🔜
Interactive scratch-off cards revealing hidden prizes.
- 🎟️ Realistic scratch effect
- 🎁 Hidden rewards
- ✨ Particle effects
- 📊 Engagement tracking
- **Category**: `engagement` | **Status**: Coming Soon

### 3. [Memory Game](./games/memory-game/) ⚡
Classic card-matching game with customizable themes.
- 🃏 Multiple difficulty levels
- 🎨 Custom card designs
- ⏱️ Timer challenges
- 📊 Performance tracking
- **Category**: `skill` | **Status**: Ready

### 4. [Slot Machine](./games/slot-machine/) ⚡ **v2.0 Compliant**
A classic 3-reel slot machine with dynamic tiered rewards.
- 🎰 3 spinning reels with weighted symbols
- 🏆 Dynamic tier system (Bronze/Silver/Gold/Platinum)
- 🎊 Smooth win animations
- 📊 Advanced performance tracking
- 🧹 Memory managed
- **Category**: `reward` | **Status**: Ready | **Compliance**: ✅ v2.0

### 5. [Hit the Target](./games/hit-the-target/) 🔜
Aim and shoot game with precision challenges.
- 🎯 Multiple targets
- 🏹 Accuracy scoring
- 🎮 Power-ups
- 📊 Skill tracking
- **Category**: `skill` | **Status**: Coming Soon

## 🏗️ Game Architecture

Each game follows a standardized structure:

```javascript
// Game Configuration
const GAME_CONFIG = {
    type: "game_name",
    version: "1.0.0",
    braze_category: "reward|engagement|skill",
    session_id: "timestamp_randomstring"
};

// Standardized Classes
- BrazeGameTracker    // Event handling
- BrazeRewardSystem   // Tier-based rewards
- GameMemoryManager   // Resource cleanup
```

## 📊 Analytics Overview

All games track standardized events with nested properties:

```javascript
{
    game: {
        type: String,
        session_id: String,
        version: String
    },
    performance: {
        score: Number,
        duration_seconds: Number,
        actions_taken: Number,
        efficiency_percent: Number,
        completion_status: String
    },
    context: {
        difficulty: String,
        device_type: String,
        is_replay: Boolean
    }
}
```

## 🚀 Quick Start

1. **Choose a Game** - Browse the games directory
2. **Copy HTML** - Get the complete game file
3. **Configure in Braze**:
   - Create In-App Message
   - Select "Custom Code"
   - Choose "HTML Upload with Preview"
   - Paste the code
4. **Customize** - Modify colors, text, and rewards
5. **Deploy** - Test and launch!

## 📱 SDK Requirements

| Platform | Minimum Version | Required Config |
|----------|-----------------|-----------------|
| Web SDK | 2.5.0+ | `allowUserSuppliedJavascript: true` |
| Android | 8.0.0+ | - |
| iOS | 4.2.0+ | - |
| Swift | 5.4.0+ | - |

## 🎨 Customization

All games support:
- **Brand Colors** - Map to Braze constants
- **Text Content** - Titles, messages, CTAs
- **Rewards** - Tiers, values, and codes
- **Game Rules** - Difficulty, limits, timing
- **Analytics** - Custom attributes and events

## 📈 Performance

| Metric | Target | Typical |
|--------|--------|---------|
| File Size | < 200KB | ~30-50KB |
| Load Time | < 2s | 1-1.5s |
| Frame Rate | 60fps | 60fps |
| Memory | < 50MB | 20-35MB |

## 🛠️ Development

### Contributing
See [CONTRIBUTING.md](./CONTRIBUTING.md) for guidelines.

### Testing Checklist
- [ ] SDK version compatibility
- [ ] Event structure validation
- [ ] Performance metrics accuracy
- [ ] Memory cleanup verification
- [ ] Cross-browser testing
- [ ] Mobile responsiveness
- [ ] Accessibility compliance

## 📄 License

MIT License - See [LICENSE](./LICENSE) for details.

## 🤝 Support
- 📚 [Braze Documentation](https://www.braze.com/docs)
- 💬 [GitHub Issues](https://github.com/VincentSolconBraze/braze-games-library/issues)
- 🎮 [Game Examples](https://github.com/braze-inc/in-app-message-templates)

---

**Braze Games Library v2.0** | Standardized Analytics | Dynamic Rewards | Full Compliance