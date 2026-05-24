# Cybersecurity Awareness Chatbot — Part 2 (WinForms GUI)

## How to Open & Run

1. Copy the `CybersecurityChatBot_Part2` folder into your existing Part 1 solution folder  
   (or open the `.csproj` as a new project inside your existing solution in Visual Studio).
2. Copy your existing `Assets/` folder (greeting.wav, question.wav, closing.wav, cyber-lock.jpg)  
   into the Part 2 project folder — the build will copy them automatically.
3. Open `CybersecurityChatBot.csproj` in Visual Studio 2019/2022.
4. Set target framework to **.NET Framework 4.7.2** (already set in .csproj).
5. Press **F5** to build and run.

> No NuGet packages required — only standard System.Windows.Forms / System.Drawing references.

---

## Files

| File | Purpose |
|------|---------|
| `Program.cs` | Entry point — `Application.Run(new MainForm())` |
| `MainForm.cs` | Full WinForms GUI — all controls, layout, chat bubbles, events |
| `ChatbotEngine.cs` | All chatbot logic — keywords, responses, sentiment, memory, delegates |
| `CybersecurityChatBot.csproj` | MSBuild project file (.NET Framework 4.7.2) |

---

## Part 2 Requirements Checklist

### 1. GUI Design ✅
- Full WinForms application with `MainForm`
- Dark cyber-themed colour scheme (deep navy, electric blue, green accents)
- ASCII art title rendered in `RichTextBox` using `Consolas` font
- Header panel, memory bar, quick-topic buttons, chat area, input bar, status strip
- Blinking status indicator (live timer)
- Audio: `greeting.wav` on launch, `question.wav` per response, `closing.wav` on exit

### 2. Keyword Recognition ✅  (10 keywords)
- `password`, `phishing`, `scam`, `privacy`, `malware`, `ransomware`,  
  `vpn`, `two-factor`, `data breach`, `firewall`
- Stored in `Dictionary<string, List<string>>` in `ChatbotEngine`

### 3. Random Responses ✅
- Each keyword has 3–4 responses in a `List<string>`
- `_random.Next(list.Count)` selects one randomly each time

### 4. Conversation Flow ✅
- Follow-up triggers ("tell me more", "another tip", "continue", "go on", etc.)
- `_lastTopic` tracks the current topic; follow-ups use it automatically

### 5. Memory & Recall ✅
- `Dictionary<string, string> _memory` stores `name` and `favTopic`
- Memory bar in the GUI shows remembered values in real time
- Responses personalise using remembered name and interest

### 6. Sentiment Detection ✅
- Detects: worried, scared, confused, frustrated, curious, anxious, overwhelmed
- Uses **delegate** `SentimentDetectedHandler` — fires event to update UI badge
- Immediately follows empathetic opener with a relevant tip (no re-prompt needed)

### 7. Error Handling ✅
- Default response for unrecognised input
- All audio calls wrapped in try/catch
- Empty input handled before processing
- Form does not crash on any input

### 8. Code Optimisation ✅
- **Delegates**: `SentimentDetectedHandler`, `MemoryUpdatedHandler` (custom delegate types)
- **Generic collections**: `Dictionary<string, List<string>>` for responses,  
  `Dictionary<string, string>` for memory and sentiment,  
  `List<string>` for triggers and greetings
- **OOP**: `ChatbotEngine` class (logic) separated from `MainForm` (UI)
- **Events**: engine fires events; form subscribes — clean separation of concerns
