# 🤝 Contributing to Braze Games Library

Thank you for your interest in contributing to the Braze Games Library! This guide will help you create games that meet our standards.

## 📋 Game Requirements

### Technical Standards

1. **Pure Vanilla Stack**
   - HTML5 (semantic markup)
   - CSS3 (with variables)
   - JavaScript (ES6+, no frameworks)
   - No external dependencies

2. **Braze Integration**
   ```javascript
   // Required: Wait for bridge
   window.addEventListener("ab.BridgeReady", function() {
       initializeGame();
   }, false);
   
   // Required: Track events
   brazeBridge.logCustomEvent("game_action", {data});
   brazeBridge.logClick("button_name");
   brazeBridge.requestImmediateDataFlush();
   ```

3. **Performance**
   - Total size < 50KB
   - Load time < 2s on 3G
   - 60fps animations
   - No memory leaks

4. **Compatibility**
   - Responsive design
   - iOS/Android support
   - Offline capability
   - Cross-browser testing

5. **Accessibility**
   - Keyboard navigation
   - ARIA labels
   - Color contrast 4.5:1
   - Screen reader support

### File Structure

```
games/
└── your-game-name/
    ├── index.html          # Game file
    ├── README.md           # Documentation
    ├── preview.png         # Screenshot
    └── examples/           # Usage examples
```

## 🎮 Creating a New Game

### 1. Fork & Clone
```bash
git clone https://github.com/YOUR_USERNAME/braze-games-library
cd braze-games-library
```

### 2. Create Game Directory
```bash
mkdir games/your-game-name
cd games/your-game-name
```

### 3. Use This Template

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Your Game Name</title>
    <style>
        :root {
            --primary-color: #FF6B35;
            --secondary-color: #F7931E;
            /* More variables */
        }
        
        /* Your styles here */
    </style>
</head>
<body>
    <div id="game-container" role="main" aria-label="Game Name">
        <!-- Game content -->
    </div>
    
    <script>
        // Wait for Braze
        window.addEventListener("ab.BridgeReady", function() {
            initializeGame();
        }, false);
        
        function initializeGame() {
            // Track game open
            if (typeof brazeBridge !== 'undefined') {
                brazeBridge.logCustomEvent("game_opened");
            }
            
            // Game logic here
        }
        
        // Handle offline mode
        if (typeof brazeBridge === 'undefined') {
            document.addEventListener('DOMContentLoaded', initializeGame);
        }
    </script>
</body>
</html>
```

### 4. Required Analytics

Your game must track:
- `game_opened` - When loaded
- `game_started` - When user begins
- `game_action` - Key interactions
- `game_completed` - When finished
- `game_closed` - On exit

### 5. Documentation

Create a README.md with:
- Game description
- Features list
- Customization guide
- Analytics events
- Use cases
- Troubleshooting

## 🧪 Testing Checklist

- [ ] Works in Braze Preview
- [ ] Responsive on all devices
- [ ] Keyboard accessible
- [ ] Analytics tracking works
- [ ] No console errors
- [ ] Performance < 50KB
- [ ] Offline compatible
- [ ] Cross-browser tested

## 📤 Submitting Your Game

1. **Test thoroughly** in Braze
2. **Add examples** of customization
3. **Update main README** to list your game
4. **Create Pull Request** with:
   - Game name and description
   - Screenshot/GIF
   - Testing confirmation

## 🎯 Quality Standards

### Code Quality
- Clean, commented code
- Consistent formatting
- Error handling
- Performance optimized

### User Experience
- Intuitive controls
- Clear instructions
- Engaging gameplay
- Smooth animations

### Braze Best Practices
- Proper event naming
- Meaningful analytics
- User attribute updates
- Efficient data flushing

## 💡 Game Ideas

Looking for inspiration?
- 🎰 Slot Machine
- 🎲 Dice Games
- 🃏 Card Games
- 🎯 Target Games
- 🧩 Puzzle Games
- ⏱️ Timer Challenges
- 🎪 Prize Pickers
- 🎮 Mini Arcade Games

## 🤔 Questions?

Open an issue or reach out in discussions. We're here to help!

---

Happy coding! 🚀