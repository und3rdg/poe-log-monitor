# poe-log-monitor
Monitors Path of Exile's log file and emits events containing the most important data when something happens in game.

## Contents

- [Getting Started](#getting-started)
- [Methods](#methods)
- [Events](#events)

## Getting Started
**Install with npm:**
```bash
$ npm install poe-log-monitor
```

**Usage:**
```javascript
var PathOfExileLog = require('poe-log-monitor');

var poeLog = new PathOfExileLog({
    logfile: "C:/Program Files (x86)/Grinding Gear Games/Path of Exile/logs/Client.txt",
    interval: 100
});

poeLog.on('message', (data) => {
    console.log(data.name + ' sent a message in ' + data.channel + ' chat: ' + data.message);
});
```

## Methods

### Constructor([options])
- `options` - An optional object containing some of the following options
    - `logfile` - The path to Path of Exile's Client.txt
    - `interval` - (default: 1000) Interval, in milliseconds, to check for changes in the log file

Constructs a new `PathOfExileLog`. If the path to the log file is valid, the script will automatically start monitoring it. You can pause or resume monitoring using the `pause()` or `start()` method respectively.

### pause()
Pauses monitoring the logfile.

### start()
Resumes monitoring the logfile.

## Events

The parameters listed below each event are stored in an object emitted by the event.

### start

Emitted when the script resumes monitoring the log file.

### pause

Emitted when the script pauses monitoring the log file.

### area
- `area` - The name of the area that has been entered

Emitted when the player enters an area.

### afk
- `isAfk` - `true` if the player is AFK
- `autoReply` - The auto reply set by the player

Emitted when the players AFK status changes.

### level
- `name` - Name of the player
- `characterClass` - Character class of the player
- `level` - Level of the player after level up

Emitted when the player levels up.

### message
- `channel` - Channel in which the message appeared
    - Can be `global`, `trade`, `party`, `guild`, `local`
- `guild` - Guild tag of the player who sent the message, if present
- `name` - Name of the player who sent the message
- `message` - Message the player sent

Emitted when a message appears in any of the active chat channels.

### whisper
- `direction` - Direction of the whispered message
	- `To` if the whisper is outgoing or `From` if the whisper is incoming
- `guild` - Guild tag of the player who sent the whisper, if present
- `name` - Name of the player who sent the whisper
- `message` - Message the player sent

Emitted when a whisper is received or sent.