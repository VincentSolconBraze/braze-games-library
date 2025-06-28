# 🤝 Contributing to Braze Games Library (v2.0)

Thank you for your interest in contributing to the Braze Games Library! This guide will help you create games that meet our v2.0 compliance standards.

## 📋 v2.0 Game Requirements

### Compliance Standards

All games MUST implement these v2.0 requirements:

1. **Standardized Classes**
   ```javascript
   // REQUIRED: All games must include
   - BrazeGameTracker    // Event handling
   - BrazeRewardSystem   // Tier-based rewards
   - GameMemoryManager   // Resource cleanup
   ```

2. **Event Structure**
   ```javascript
   // REQUIRED: Nested object format
   {
       game: {
           type: "game_name",
           session_id: "timestamp_randomstring",
           version: "1.0.0"
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

3. **CSS Variables**
   ```css
   :root {
       /* REQUIRED: Braze Brand Colors (NON MODIFIABLE) */
       --braze-orange: #FFA524;
       --braze-pink: #FFA4FB;
       --braze-purple: #801ED7;
       
       /* Game colors mapped to Braze */
       --game-primary: var(--braze-orange);
       --game-secondary: var(--braze-pink);
       --game-accent: var(--braze-purple);
   }
   ```

### Technical Standards

1. **Pure Vanilla Stack**
   - HTML5 (semantic markup)
   - CSS3 (with Braze variables)
   - JavaScript (ES6+, no frameworks)
   - No external dependencies

2. **Braze Integration**
   ```javascript
   // REQUIRED: Standard initialization
   let gameTracker;
   
   window.addEventListener("ab.BridgeReady", function() {
       initializeGame();
   }, false);
   
   function initializeGame() {
       gameTracker = new BrazeGameTracker(GAME_CONFIG);
       gameTracker.trackEvent('game_opened');
       // Initialize game
   }
   ```

3. **Performance**
   - Total size < 200KB
   - Load time < 2s on 3G
   - 60fps animations
   - Memory managed via GameMemoryManager

4. **SDK Requirements**
   - Web: 2.5.0+ with `allowUserSuppliedJavascript: true`
   - Android: 8.0.0+
   - iOS: 4.2.0+

5. **Accessibility**
   - WCAG 2.1 compliance
   - Keyboard navigation
   - ARIA labels
   - Screen reader support

### File Structure

```
games/
└── your-game-name/
    ├── your-game-index.html    # Game file (v2.0 compliant)
    ├── your-game-readme.md     # Documentation
    ├── your-game-customization.md  # Customization guide
    └── preview.png             # Screenshot (16:9 ratio)
```

## 🎮 Creating a New Game

### 1. Fork & Clone
```bash
git clone https://github.com/YOUR_USERNAME/braze-games-library
cd braze-games-library
```

### 2. Use v2.0 Template

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{{GAME_NAME}} - Braze Interactive Game</title>
    <style>
        /* OBLIGATOIRE : Variables CSS Braze-compatibles */
        :root {
            /* Braze Brand Colors (NON MODIFIABLE) */
            --braze-orange: #FFA524;
            --braze-pink: #FFA4FB;
            --braze-purple: #801ED7;
            
            /* Customizable Game Colors */
            --game-primary: var(--braze-orange);
            --game-secondary: var(--braze-pink);
            --game-accent: var(--braze-purple);
            --game-background: #FFFFFF;
            --game-text: #333333;
            
            /* Performance Variables */
            --transition-speed: 0.3s;
            --border-radius: 12px;
            --shadow-depth: 0 4px 20px rgba(0,0,0,0.1);
        }
        
        /* OBLIGATOIRE : Base responsive */
        * { box-sizing: border-box; margin: 0; padding: 0; }
        body { 
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Arial, sans-serif;
            overflow: hidden;
            background: var(--game-background);
        }
        
        #game-container {
            width: 100vw;
            height: 100vh;
            max-width: 500px;
            max-height: 800px;
            margin: 0 auto;
            position: relative;
            display: flex;
            flex-direction: column;
        }
        
        /* OBLIGATOIRE : Close button standardisé */
        #close-btn {
            position: absolute;
            top: 10px;
            right: 10px;
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: rgba(255,255,255,0.9);
            border: 2px solid var(--game-primary);
            color: var(--game-primary);
            font-size: 20px;
            cursor: pointer;
            z-index: 1000;
            transition: all var(--transition-speed);
        }
        
        #close-btn:hover { transform: scale(1.1); }
        
        /* OBLIGATOIRE : Accessibility */
        .sr-only {
            position: absolute;
            width: 1px;
            height: 1px;
            padding: 0;
            margin: -1px;
            overflow: hidden;
            clip: rect(0, 0, 0, 0);
            white-space: nowrap;
            border: 0;
        }
        
        button:focus, [tabindex]:focus {
            outline: 3px solid var(--game-primary);
            outline-offset: 2px;
        }
    </style>
</head>
<body>
    <div id="game-container" role="main" aria-label="{{GAME_NAME}} Interactive Game">
        <button id="close-btn" aria-label="Close game" onclick="closeGame()">×</button>
        
        <div class="game-content">
            <!-- Your game content here -->
        </div>
        
        <div class="sr-only" role="status" aria-live="polite" id="sr-status"></div>
    </div>
    
    <script>
        // OBLIGATOIRE : Configuration du jeu
        const GAME_CONFIG = {
            type: "{{GAME_TYPE}}",
            version: "1.0.0",
            braze_category: "{{CATEGORY}}", // reward|engagement|skill
            session_id: Date.now() + '_' + Math.random().toString(36).substr(2, 9)
        };
        
        // OBLIGATOIRE : Include standardized classes
        // [Include BrazeGameTracker class here]
        // [Include BrazeRewardSystem class here]
        // [Include GameMemoryManager class here]
        
        // OBLIGATOIRE : Initialisation Braze
        let gameTracker;
        let rewardSystem;
        let memoryManager;
        
        window.addEventListener("ab.BridgeReady", function() {
            initializeGame();
        }, false);
        
        // Fallback pour test hors Braze
        if (typeof brazeBridge === 'undefined') {
            document.addEventListener('DOMContentLoaded', initializeGame);
        }
        
        function initializeGame() {
            gameTracker = new BrazeGameTracker(GAME_CONFIG);
            rewardSystem = new BrazeRewardSystem(GAME_CONFIG.type);
            memoryManager = new GameMemoryManager();
            
            gameTracker.trackEvent('game_opened');
            
            // Your game initialization here
            setupGame();
        }
        
        function closeGame() {
            // Calculate final performance
            const performance = calculatePerformance();
            
            gameTracker.trackClick('close_button');
            gameTracker.trackEvent('game_closed', {
                performance: performance
            });
            
            // Cleanup
            memoryManager.cleanup();
            
            if (typeof brazeBridge !== 'undefined') {
                brazeBridge.closeMessage();
            }
        }
        
        function setupGame() {
            // Your game logic here
        }
        
        function calculatePerformance() {
            // Return standardized performance object
            return {
                score: 0,
                duration_seconds: Math.floor((Date.now() - gameTracker.startTime) / 1000),
                actions_taken: gameTracker.actionCount,
                efficiency_percent: 0,
                completion_status: 'abandoned'
            };
        }
        
        // OBLIGATOIRE : Gestion des erreurs
        window.addEventListener('error', function(e) {
            gameTracker?.trackEvent('game_error', {
                error: {
                    message: e.message,
                    filename: e.filename,
                    line: e.lineno
                }
            });
        });
    </script>
</body>
</html>
```

### 3. Required Analytics Events

Your game MUST track these standardized events:

| Event | When | Required Data |
|-------|------|---------------|
| `game_opened` | Page load | session_id |
| `game_started` | First action | device_type |
| `game_action` | Each interaction | action details |
| `game_completed` | Game ends | performance metrics |
| `reward_earned` | Win occurs | tier, code |
| `reward_claimed` | Claim button | reward details |
| `game_closed` | Exit | final metrics |
| `game_error` | JS errors | error info |

### 4. Performance Metrics

Calculate and track:
- **score**: Points/value achieved
- **duration_seconds**: Total play time
- **actions_taken**: Number of interactions
- **efficiency_percent**: Performance ratio (0-100)
- **completion_status**: `completed`, `failed`, or `abandoned`

### 5. Reward System

Implement tier-based rewards:
- **Bronze** (0-33%): Entry level
- **Silver** (34-66%): Standard
- **Gold** (67-89%): Premium
- **Platinum** (90-100%): Top tier

## 🧪 Testing Checklist

### Compliance Testing
- [ ] BrazeGameTracker implemented
- [ ] BrazeRewardSystem integrated
- [ ] GameMemoryManager active
- [ ] Nested event structure
- [ ] Standardized event names
- [ ] Performance metrics tracked
- [ ] Braze CSS variables used
- [ ] Session ID format correct

### Technical Testing
- [ ] Works in Braze Preview
- [ ] SDK version compatible
- [ ] Memory cleanup verified
- [ ] No console errors
- [ ] < 200KB total size
- [ ] Offline compatible
- [ ] Error handling works

### UX Testing
- [ ] Responsive on all devices
- [ ] Keyboard accessible
- [ ] Screen reader compatible
- [ ] 60fps animations
- [ ] Clear instructions
- [ ] Intuitive controls

## 📤 Submitting Your Game

1. **Validate Compliance**
   - Run through v2.0 checklist
   - Test all required events
   - Verify performance tracking

2. **Documentation**
   - README with compliance badge
   - Customization guide
   - Event mapping table
   - Performance benchmarks

3. **Create Pull Request**
   ```
   Title: [NEW GAME] Game Name - v2.0 Compliant
   
   Description:
   - Game type: reward|engagement|skill
   - Compliance: ✅ v2.0
   - Testing: Confirmed on [platforms]
   - Analytics: All events implemented
   ```

## 🎯 Quality Standards

### Code Quality
- Clean, documented code
- Standardized formatting
- Error boundaries
- Memory management
- Performance optimized

### Analytics Quality
- Meaningful metrics
- Accurate tracking
- Proper attribution
- Efficient flushing

### User Experience
- Fast loading
- Smooth animations
- Clear feedback
- Accessible design
- Mobile optimized

## 💡 Game Categories

Choose the appropriate category:

### 🎁 Reward Games
- Slot machines
- Wheel spinners
- Scratch cards
- Prize reveals

### 🎮 Engagement Games
- Memory matching
- Trivia challenges
- Puzzle solving
- Pattern recognition

### 🎯 Skill Games
- Target shooting
- Reaction timing
- Precision tasks
- Speed challenges

## 🚀 Advanced Features

Consider adding:
- Progressive difficulty
- Leaderboards
- Achievement system
- Social sharing
- Save states
- Multiplayer modes

## 🤔 Questions?

- Check existing games for examples
- Review compliance documentation
- Open an issue for help
- Join our discussions

---

**Remember**: v2.0 compliance is mandatory for all new games. Games not meeting these standards will not be accepted.

Happy coding! 🚀