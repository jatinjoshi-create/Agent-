# SafeNet – Cyberbullying Prevention App (Scratch Project Blueprint)

This guide gives you a complete, app-style Scratch project with **3 screens**: **Home**, **Chat**, and **Result**.

---

## 1) Project Setup

### Sprites to create
1. `UI_Controller` (can be invisible; controls logic)
2. `StartButton`
3. `ReportButton`
4. `StatusText` (optional helper sprite for extra labels)

### Backdrops to create (Stage)
Create 4 backdrops with clean mobile-style layout:
1. `Home`
2. `Chat`
3. `ResultSafe`
4. `ResultBullying`

Use simple colors and rounded shapes:
- Home: white/light background with green accent
- Chat: messaging-style panel and header
- ResultSafe: green theme
- ResultBullying: red theme

---

## 2) Variables

Create variables **for all sprites**:
- `message`
- `badCount`
- `isHarmful`

Initialize values on green flag:
- `message = ""`
- `badCount = 0`
- `isHarmful = 0`

---

## 3) Broadcast Events (Navigation)

Create broadcasts:
- `goHome`
- `goChat`
- `checkMessage`
- `showSafeResult`
- `showBullyingResult`

Flow:
- Green Flag → `goHome`
- Start button clicked → `goChat`
- Chat input complete → `checkMessage`
- Detection → `showSafeResult` OR `showBullyingResult`

---

## 4) Stage / UI Design Details

### Home Backdrop
Add text:
- **SafeNet 🛡️** (large title)
- **Stay Safe Online** (subtitle)

Add a rounded green Start button sprite centered near bottom.

### Chat Backdrop
Design like chat app:
- Top bar title: **Chat Checker**
- Message input area visual (just UI drawing)
- Optional chat bubble icon

### ResultSafe Backdrop
Green theme text:
- **✅ Safe Message!**
- **Always be kind online 😊**
- Show variable monitor for `badCount`

### ResultBullying Backdrop
Red theme text:
- **⚠️ Bullying Detected!**
- **Don’t reply angrily**
- **Block or report the user**
- **Talk to a parent or teacher**
- Show variable monitor for `badCount`

---

## 5) Core Scratch Code

## A) `UI_Controller` sprite scripts

### Script 1: App start
```scratch
when green flag clicked
set [message v] to []
set [badCount v] to [0]
set [isHarmful v] to [0]
broadcast [goHome v]
```

### Script 2: Home navigation
```scratch
when I receive [goHome v]
switch backdrop to [Home v]
```

### Script 3: Chat navigation + ask input
```scratch
when I receive [goChat v]
switch backdrop to [Chat v]
ask [Type a message to analyze:] and wait
set [message v] to (answer)
broadcast [checkMessage v]
```

### Script 4: Detection system with “Checking...” delay
```scratch
when I receive [checkMessage v]
set [isHarmful v] to [0]

say [Checking...] for (1) seconds

if <(message) contains [stupid]> then
  set [isHarmful v] to [1]
end
if <(message) contains [loser]> then
  set [isHarmful v] to [1]
end
if <(message) contains [hate]> then
  set [isHarmful v] to [1]
end
if <(message) contains [ugly]> then
  set [isHarmful v] to [1]
end
if <(message) contains [idiot]> then
  set [isHarmful v] to [1]
end

if <(isHarmful) = [1]> then
  change [badCount v] by (1)
  broadcast [showBullyingResult v]
else
  broadcast [showSafeResult v]
end
```

> Tip: To make matching stronger, you can convert text to lowercase with an extension or by asking users to type in lowercase.

### Script 5: Show safe result
```scratch
when I receive [showSafeResult v]
switch backdrop to [ResultSafe v]
```

### Script 6: Show bullying result
```scratch
when I receive [showBullyingResult v]
switch backdrop to [ResultBullying v]
```

---

## B) `StartButton` sprite scripts

### Costume/UI
- Rounded rectangle, green fill
- Text: `Start`

### Logic
```scratch
when green flag clicked
show
```

```scratch
when I receive [goHome v]
show
```

```scratch
when I receive [goChat v]
hide
```

```scratch
when I receive [showSafeResult v]
hide
```

```scratch
when I receive [showBullyingResult v]
hide
```

```scratch
when this sprite clicked
broadcast [goChat v]
```

---

## C) `ReportButton` sprite scripts

### Costume/UI
- Rounded red/orange button
- Text: `Report`

### Logic
```scratch
when green flag clicked
hide
```

```scratch
when I receive [showBullyingResult v]
show
```

```scratch
when I receive [goHome v]
hide
```

```scratch
when I receive [goChat v]
hide
```

```scratch
when I receive [showSafeResult v]
hide
```

```scratch
when this sprite clicked
say [Reported Successfully 🚨] for (2) seconds
```

---

## 6) Interaction Notes (for school demo)

Demo script:
1. Click green flag → Home appears with SafeNet branding.
2. Click Start → Chat screen opens.
3. Enter safe text like: `you are awesome` → Safe result.
4. Repeat with harmful text like: `you are stupid` → Bullying result + report option.
5. Click Report → confirmation appears.
6. Show `badCount` increasing to demonstrate monitoring.

---

## 7) Why this is a real-world STEAM solution

- **Problem-solving:** identifies harmful language patterns.
- **Technology/AI logic:** rule-based text detection simulating moderation AI.
- **User interaction:** app-like flow with buttons, chat input, and dynamic result screens.
- **Real-world relevance:** teaches digital safety and encourages responsible reporting.

---

## 8) Optional polish ideas

- Add `Try Again` button on result screens to return to chat.
- Add sound effects: short notification on safe / alert tone on bullying.
- Add more harmful keywords.
- Save last analyzed message in a list for teacher review demo.
