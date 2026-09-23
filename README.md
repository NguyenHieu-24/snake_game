<h1 align="center">Snake Game</h1>
<p align="center">
  A single-player Java desktop game built to explore data structures and algorithms.
</p>
<p align="center">
  <img src="https://img.shields.io/badge/Language-Java-ED8B00?style=flat-square" alt="Language: Java">
  <img src="https://img.shields.io/badge/GUI-Swing%20%2F%20AWT-0078D4?style=flat-square" alt="GUI: Swing / AWT">
  <img src="https://img.shields.io/badge/Tests-JUnit%204-25A162?style=flat-square" alt="Tests: JUnit 4">
  <img src="https://img.shields.io/badge/Status-Educational%20Prototype-F2C94C?style=flat-square" alt="Status: Educational prototype">
</p>
<p align="center">
  <a href="#overview">Overview</a> ·
  <a href="#features">Features</a> ·
  <a href="#quick-start">Quick Start</a> ·
  <a href="#how-to-play">How to Play</a> ·
  <a href="#architecture">Architecture</a> ·
  <a href="#known-issues">Known Issues</a>
</p>

---

# Overview
Guide the snake across a grid, collect food to grow and score points, and avoid walls and your own body. Developed as a Data Structures and Algorithms project, the game uses a two-dimensional board, an ordered list of body segments, timed movement, and a persistent leaderboard.

> **Project variant:** Choose Easy, Medium, or Hard. At the end of a round, you can save a score under your username and view the top five scores for the selected difficulty.

---

# Features

| | Feature | Implementation |
| :---: | --- | --- |
| 🐍 | Snake movement | Arrow keys or WASD; reverse turns are blocked |
| 🍎 | Food and growth | Random food placement; one point and one segment per food |
| 🧱 | Collision handling | Wall and body collisions end the round |
| ⚙️ | Difficulty | Easy (100 ms), Medium (75 ms), Hard (50 ms) between ticks |
| 🏆 | Leaderboard | Scores saved in `highscores.txt`; top five per difficulty |
| 🖥️ | Desktop interface | Start, Settings, Help, game, and score screens |
| 🧪 | Tests | Five JUnit 4 tests covering movement and game rules |

---

# Quick Start
## 1. Prepare your environment
- Install a JDK with `java` and `javac` available in your terminal.
- Use a graphical desktop environment.
- Download or clone the repository and keep `src/`, `images/`, `lib/`, and `highscores.txt` together.

Open a terminal **in the repository root**, the folder containing `src/`:
```sh
java -version
javac -version
```

The source uses the Java standard library for gameplay. The included JUnit JAR is needed when compiling `src/GameTest.java` with the rest of `src/`.

## 2. Compile and launch
```sh
mkdir build
javac -encoding UTF-8 -cp "lib/junit-platform-console-standalone-1.11.3.jar" -d build src/*.java
java -cp build Game
```

Skip `mkdir build` if the directory exists. Keep the repository root as your working directory so the game can locate `highscores.txt` and menu images.

<details>
<summary><strong>Using Visual Studio Code</strong></summary>
<ol>
<li>Open the folder containing <code>`src/`</code>, <code>`images/`</code>, and <code>`lib/`</code> as the workspace.</li>
<li>Select an installed JDK and open the integrated terminal.</li>
<li>Run the commands above.</li>
<li>If using a launch configuration, set `Game` as the main class and the repository root as the working directory.</li>
<ol>
</details>

<details>
<summary><strong>Troubleshooting</strong></summary>

| Symptom | Check |
| --- | --- |
| `javac` is not recognized | Install a JDK and add its `bin` directory to your terminal path. |
| JUnit imports cannot be resolved | Include `lib/junit-platform-console-standalone-1.11.3.jar` on the compilation classpath. |
| Menu images are missing on macOS/Linux | Replace Windows-style paths such as `images\\button_start.png` with `images/button_start.png` in menu classes. |
| High scores cannot be saved | Run from the repository root and ensure `highscores.txt` is writable. |
| Snake does not respond to keys | Click the game area to give it keyboard focus, then press Enter. |

**Validation:** The README was checked against the supplied source and filenames. Compilation and gameplay were not verified here because `javac` was unavailable.

</details>

---

# How to Play

| Step | Action |
| --- | --- |
| **1** | Select **Settings** to choose a difficulty, or use the default **Easy** level. |
| **2** | Select **Start**, then press **Enter** to begin the round. |
| **3** | Use the **arrow keys** or **WASD** to guide the snake toward food. |
| **4** | Avoid walls and body segments; each food increases your score by one. |
| **5** | After game over, press **Enter** to open the score screen. Enter a username and select **Save** or **Show Highscores**. |

<details>
<summary><strong>Controls and game rules</strong></summary>

| Input / rule | Current behavior |
| --- | --- |
| ↑ / W, ↓ / S, ← / A, → / D | Change direction; an immediate reversal is blocked |
| Enter before play | Start the round |
| Enter after game over | Open the score screen |
| Esc during play | End the current round; this does not pause the game |
| Esc after game over | Exit the application |
| Board | 30 columns × 25 rows; snake starts with three segments |
| Food | Adds one point and one body segment, then respawns |
| Easy / Medium / Hard | Timer delays of 100 / 75 / 50 ms |
| Collision | Hitting a wall or body segment ends the round |

</details>

---

# Architecture

| Class | Responsibility |
| --- | --- |
| `Game` | Entry point, window, selected difficulty, and screen navigation |
| `GameLogic` | Game timer, keyboard input, movement, food, collisions, and scoring |
| `Board` | Two-dimensional grid and board rendering |
| `GameObj` | Base class for board entities |
| `Snake`, `FoodObj` | Snake segments and food entities |
| `InfoPanel` | Current score display |
| `StartMenu`, `SettingsMenu`, `HelpMenu` | Menu screens |
| `EndMenu`, `HighScoreUpdater` | Score entry, file storage, and leaderboard |
| `GameTest` | JUnit test cases |

<details>
<summary><strong>Data structures and algorithms</strong></summary>

| Concept | Use in this project |
| --- | --- |
| Two-dimensional array | `GameObj[][]` stores the object occupying each board cell |
| Dynamic array | `ArrayList<Snake>` maintains the head and ordered body segments |
| Ordered maps | Three case-insensitive `TreeMap<String, Integer>` instances retain best scores by difficulty |
| Enums | `Direction` and `Type` represent movement and entity types |
| Timer-driven updates | A Swing `Timer` triggers movement and collision checks |
| Random food placement | Selects a free cell after food is consumed |
| Score sorting | Sorts leaderboard entries by descending value before showing the top five |

With **N** snake segments on an **R × C** board, moving all segments is O(N), checking the next grid cell is O(1), and rebuilding or drawing the board scans O(RC) cells. Food respawn can also scan O(RC) cells. These are bounds for the described operations, not measured performance.

</details>

---

# Project Files

| Path | Contents |
| --- | --- |
| `src/` | Java application classes and JUnit test class |
| `images/` | Menu images and backgrounds |
| `highscores.txt` | Saved username, score, and difficulty records |
| `lib/junit-platform-console-standalone-1.11.3.jar` | Bundled JUnit test runner |
| `out/` | Previously compiled output; Quick Start creates fresh classes in `build/` |

---

# Testing
To run the included tests after compiling:
```sh
java -jar lib/junit-platform-console-standalone-1.11.3.jar execute --class-path build --select-class GameTest
```

| Test | Intended coverage |
| --- | --- |
| `testSnakeWillHitWall` | Wall detection |
| `testGameWillEndHitWall` | Wall collision outcome |
| `testGameWillEndEatBody` | Body collision outcome |
| `testMoveSnake` | Segment movement and board update |
| `testEatFood` | Food collection, growth, and respawn |

The test JAR is included, but these tests were **not executed** in the review environment. The badge identifies the framework, not a passing test result.

---

# Known Issues
**Educational prototype:** the repository contains two Snake implementations, platform-specific image paths, and test cases that need stronger assertions.

<details>
<summary><strong>View source-review findings</strong></summary>

| Area | Finding |
| --- | --- |
| Duplicate implementation | `GamePanel.java` implements a separate Snake game; the documented controls and rules refer to the menu-driven `GameLogic` flow. |
| Missing assets | `GamePanel.java` refers to `src/resources/` images that are absent from the supplied archive. |
| Image portability | Menu classes use Windows backslashes in image paths. |
| Replay | The end screen offers Save, Exit, and Show Highscores; replay assets are not wired into that flow. |
| Food spawning | A full board has no explicit completion state when no free cells remain. |
| Score file | Input and file format need validation; usernames containing commas break the record format. |
| Resource handling | The score writer is not closed if a score is rejected as equal or lower. |
| Tests | Some tests copy production logic; the food-respawn assertion can fail for a valid position that shares one coordinate with the previous food. |
| Attribution | Multiple source files contain CIS 120 Game HW headers; `images/README.txt` contains related course-project notes. |

</details>

---

# Roadmap
- Consolidate the two Snake implementations.
- Load images through portable resource paths.
- Add replay and pause/resume to the main game flow.
- Handle a full board and validate score records.
- Make tests deterministic and test production methods directly.

---

# Contributing
Open an issue or submit a focused pull request. Include reproduction steps, Java version, operating system, and how you checked your change.

# Acknowledgments and License
Several source files retain **University of Pennsylvania CIS 120 Game HW** headers, and `images/README.txt` contains related project notes. Preserve this attribution when extending the repository.

The supplied archive has no `LICENSE` file. Maintainers should confirm permissions for the source and images before specifying license terms.

---

<p align="center"><a href="#snake-game">Back to top ↑</a></p>
