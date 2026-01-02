# Wordle HTML Browser Source Display Guide

## How It Works

When using the **WordleHtmlCommand.cs** version of Wordle, every time a player makes a guess, the command automatically generates/updates an HTML file that displays the current game state. This HTML file can be added as a **Browser Source** in OBS to show on your stream.

## What It Looks Like

The HTML display includes:

### 1. Title
- **"HexEchoTV"** on the first line
- **"Wordle Challenge"** on the second line
- Large, glowing purple text at the top
- Purple border with glow effect around the entire container
- Dark semi-transparent background

### 2. Word Display
- Shows **"? ? ? ? ?"** while the game is in progress (hidden word)
- Shows the **actual word** when the game ends (win or lose)
- Large, bold, centered text with white glow

### 3. Guess Grid
- Each guess appears as a row of 5 colored squares
- Each square shows a letter with a colored background:
  - **🟩 Green (Correct):** Letter is in the word AND in the correct position
  - **🟨 Yellow (Present):** Letter is in the word but in the WRONG position
  - **⬛ Gray/Black (Absent):** Letter is NOT in the word at all
- Matches the real Wordle game colors and style

### 4. Game Status
- **During Game:** Shows "Guesses Remaining: X/6"
- **On Win:** Shows "🎉 [Username] WON! 🎉" in green text
- **On Loss:** Shows "❌ Game Over ❌" in red text and reveals the word

## Example Visual Breakdown

```
╔═══════════════════════════════════════════════════╗
║                                                   ║
║       HexEchoTV Wordle Challenge                 ║  ← Purple glowing title
║                                                   ║
║              ? ? ? ? ?                            ║  ← Hidden word (or revealed)
║                                                   ║
║         [C][R][A][N][E]                          ║  ← Guess 1
║          🟩⬛🟨⬛⬛                                ║
║                                                   ║
║         [C][O][A][S][T]                          ║  ← Guess 2
║          🟩⬛🟩⬛⬛                                ║
║                                                   ║
║         [C][H][A][R][M]                          ║  ← Guess 3
║          🟩🟩🟩🟩🟩                                ║
║                                                   ║
║         🎉 UserName WON! 🎉                       ║  ← Win message
║                                                   ║
╚═══════════════════════════════════════════════════╝
     Purple border with glow effect
```

## Color Scheme

- **Background:** Dark semi-transparent black (rgba(0, 0, 0, 0.85))
- **Border:** Purple (#6c63ff) with glowing shadow
- **Title:** Purple (#6c63ff) with glow effect
- **Word Display:** White with glow
- **Correct Letters:** Green background (#538d4e)
- **Present Letters:** Yellow/Gold background (#b59f3b)
- **Absent Letters:** Dark gray background (#3a3a3c)
- **Win Text:** Green (#538d4e)
- **Loss Text:** Red (#ff6b6b)

## OBS Setup Steps

1. **Add Browser Source:**
   - In OBS, add a new **Browser Source** to your scene
   - Local File: Browse to your `wordle.html` file
     - Or use URL: `file:///C:/Path/To/Your/wordle.html`
   - Width: **800** (recommended)
   - Height: **600** (recommended)
   - Check ✅ **"Refresh browser when scene becomes active"**

2. **Position & Size:**
   - Drag and resize in OBS to fit your layout
   - Works great in the corner or as a full overlay
   - The container auto-sizes to content

3. **Transparency:**
   - The background is transparent outside the main container
   - Only the dark panel with purple border will show
   - Perfect for overlaying on your stream

## How It Updates

The HTML file auto-refreshes every 2 seconds using JavaScript, so OBS picks up changes automatically!

1. **Game Start:**
   - Player types `!wordlehtml`
   - HTML file is created showing "? ? ? ? ?" and "Guesses Remaining: 6/6"
   - OBS updates within 2 seconds

2. **Each Guess:**
   - Player types `!wordlehtml CRANE`
   - HTML file updates instantly with the new guess row and colored feedback
   - OBS refreshes automatically within 2 seconds
   - Remaining guesses counter decreases

3. **Game End (Win):**
   - Player guesses correctly
   - HTML shows all guesses, reveals the word, displays "🎉 [User] WON! 🎉"
   - Updates appear in OBS within 2 seconds

4. **Game End (Loss):**
   - Player runs out of guesses
   - HTML shows all failed attempts, reveals the word, displays "❌ Game Over ❌"

5. **Next Game:**
   - When a new player starts a game, the HTML resets to show their game

## Live Example

Open the included `sample-wordle.html` file in your browser to see exactly how it looks! This is a static example showing what the display looks like mid-game.

## Customization

You can customize the appearance by editing the `<style>` section in the `UpdateHtmlFile()` method in `WordleHtmlCommand.cs`:

### Change Colors
```css
border: 3px solid #6c63ff;  /* Purple border - change to your color */
color: #6c63ff;             /* Title color */
```

### Change Size
```css
font-size: 48px;            /* Title size */
font-size: 72px;            /* Word display size */
width: 60px;                /* Letter box width */
height: 60px;               /* Letter box height */
```

### Change Fonts
```css
font-family: 'Arial', sans-serif;  /* Change to your preferred font */
```

### Change Auto-Refresh Interval
Find the JavaScript section in the code and change the timeout:
```javascript
setTimeout(function() {
    location.reload();
}, 2000);  // Change 2000 to your desired milliseconds (2000 = 2 seconds)
```

### Add Animations
You can add CSS animations for guesses appearing, letters flipping, etc.

## Tips for Best Display

1. **Stream Overlay:**
   - Place in bottom-right or top-right corner
   - Size to about 20-25% of your stream canvas

2. **Dedicated Scene:**
   - Create a "Wordle Game" scene that focuses on the browser source
   - Switch to it when someone plays

3. **Chroma Key:**
   - If you want only the panel visible, you can use OBS color key
   - Key out the transparent areas (though they're already transparent)

4. **Refresh:**
   - Enable "Refresh browser when scene becomes active" for reliable updates
   - Or set a refresh interval in OBS browser source settings

## Troubleshooting Display Issues

**Browser source shows blank:**
- Check the file path is correct in ConfigSetup.cs
- Make sure the HTML file exists at that location
- Use forward slashes in path: `G:/Path/To/wordle.html` not `G:\Path\To\wordle.html`
- Try using absolute path in OBS: `file:///C:/Full/Path/To/wordle.html`

**Updates not showing:**
- The HTML auto-refreshes every 2 seconds via JavaScript
- Enable "Refresh browser when scene becomes active" in OBS browser source properties
- Right-click browser source → Refresh
- Check StreamerBot logs to ensure file is being written
- Verify the path in `config_wordle_html_path` is correct

**Styling looks wrong:**
- Ensure OBS browser source has enough width/height (800x600 recommended)
- Check that CSS is rendering correctly in a regular browser first
- Clear OBS browser cache: right-click source → Properties → check "Shutdown source when not visible"

**Transparent background not working:**
- OBS browser sources support transparency by default
- Make sure you haven't set a background color in OBS source settings

**Auto-refresh not working:**
- The JavaScript auto-reload runs every 2 seconds
- Check that JavaScript is enabled in OBS browser source
- Verify the HTML file contains the `<script>` tag with `location.reload()`

## Advanced: Multiple Games

If you want to show multiple players' games simultaneously:
1. Modify `config_wordle_html_path` to include username: `wordle-{user}.html`
2. Update the UpdateHtmlFile method to use the username in the filename
3. Add multiple browser sources in OBS, each pointing to a different user's file

This allows you to have multiple Wordle games visible at once!
