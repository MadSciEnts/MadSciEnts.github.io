---
title: Ai - Analysis
author: <SW>
categories: [Ai]
tags: [Android]
media_subpath: /media/
---


# Abstract

The investigation tests LLM-driven code generation for Android apps ranging from utility tools to interactive games. Direct iterative prompting with Gemini in Android Studio succeeds for simple applications but fails for complex, evolving projects due to context overload, repetitive errors, and unhandled assumptions in generated code. A meta-approach—using LLMs (notably **Grok**) to craft high-quality framework prompts for subsequent code generation—yields markedly better results, producing a basically playable game. Key limitations include poor handling of procedural textures, text legibility, orientation management, and long conversational histories. The findings highlight prompt engineering as a critical intermediary layer for improving AI-assisted mobile game development outcomes.

# Introduction

Modern LLMs demonstrate strong code-generation abilities, yet their application to full application development—especially iterative, stateful projects—remains underexplored in real-world IDE integrations like Android Studio's Gemini plugin. This work examines:

- Rapid generation of utility apps
- Feasibility of building incrementally complex 2D games
- Challenges in texture synthesis, physics, UI layout, and context management
- Comparative effectiveness of different LLMs when used to design prompts rather than write code directly

The experiments use consumer-accessible tools (Gemini in Android Studio, supplemented by ChatGPT and Grok) without external libraries beyond those suggested by the models.

# Methods

## Environment and Tools
- **IDE**: Android Studio with integrated Google Gemini
- **Models**:
  - Primary: Gemini (version/context not specified; IDE-integrated)
  - Secondary evaluators: ChatGPT, Grok (for prompt framework design)
- **Target platform**: Android mobile applications (Java/Kotlin assumed via Android Studio defaults)
- **Approach variants**:
  1. Direct iterative prompting within a single long conversation in Android Studio
  2. Meta-prompting: Instruct LLMs to output a detailed, structured prompt describing a game framework, then feed that prompt to Gemini in Android Studio

## Experiments
1. **Tone Generator App** — Simple audio utility
2. **Simple Dungeon Crawler** — Basic game with attack/block mechanics
3. **Asteroids-style Top-Down Space Game** — Physics-based game with momentum, enemies, projectiles
4. **Meta-Prompt Framework for Complex Spaceship Evolution Game** — Top-down 2.5D action game with leveling, procedural assets, multiple weapon types, HUD, parallax background

Detailed prompt used for meta-framework (quoted verbatim from source):

> "Choose a well known and effective framework for creating simple mobile video games. Similar to a simple action RPG. Describe the framework in detail in such a way that it could be used as a guide for creating a mobile game. The framework should support a 'Top Down' 2.5d game where the player controls a spaceship that has inventory and weapon ports. The player ship should 'evolve' in complexity to support increasing size and number of weapons. The weapons should be broken up into 3 categories: Projectiles, Beams, Missiles. The player and enemy classes should inherit from a common base class. On screen controls should be used. On Screen Joystick for motion. On Screen buttons for attack and manipulation of inventory. Spaceships should not have initial motion, but maintain momentum with little or no drag. Background should be of a particle based starfield that shows parallax. Color variation should be a prevalent theme denoting importance or rarity of object. Starfield should have 40% color and intensity variation. Player HUD should have progress bars for any attributes like health and shield prominently displayed. An experience counter / bar should be used/shown to indicate when player is going to level up and evolve. Textures should be procedurally generated for all HUD elements, weapons, and effects using a pixelated style. Any text should be of a 64x64 character resolution for legibility. Describe this framework as an effective prompt for the creation of a mobile game in Android Studio using Gemini ready to play."

Subsequent refinements (via Grok-generated prompt) added radar, infinite leveling (+1 weapon slot every 5 levels), charge weapon mechanic, debug level-up buttons, and visual ship scaling.

# Results

## 1. Tone Generator
- Successfully generated functional app
- Features: 500–20,000 Hz range, background execution, theme support, persistent settings
- Build errors frequent but auto-resolved by Gemini
- Outcome: Fully usable APK produced (GDDW_003.apk)

## 2. Simple Dungeon Crawler
- Core mechanics (block/attack) implemented
- Major limitation: Procedural texture generation
  - Refused text/numbers as textures
  - Defaulted to hard-coded pixel-by-pixel 8×8 textures
  - Upscaling produced illegible results (e.g., "Game Over")
- Required highly explicit prompting for legible 64×64 text
- Outcome: Basic but functional game after refinement

## 3. Asteroids-Style Game (Direct Iteration)
- Implemented momentum physics, auto-targeting, parallax starfield attempt
- Persistent issues:
  - Text rendering failures
  - Unnecessary multi-layout orientation handling
  - Projectile collision (instead of more accurate raycasting)
- Critical failure mode: **Context overload** in long conversation
  - Frequent request timeouts
  - Model repeated identical file modifications indefinitely
  - Project became permanently unbuildable
- Outcome: Complete failure for incremental evolution

## 4. Meta-Prompt Framework Approach
- **Gemini** (self-prompting): Suggested LibGDX but with incompatible libraries → infinite build-fix loop → unusable
- **Grok**: Produced coherent, structured LibGDX-based prompt → fed to Gemini → basically playable game
  - Core features: Momentum physics, on-screen joystick/buttons, HUD (health/shield/XP bars), procedural pixelated textures (64×64 text), weapon categories, inheritance structure, color variation
  - Added features (post-generation): Radar, infinite leveling, charge blast, debug controls, ship size growth
- Remaining issues: Incomplete parallax starfield implementation
- Outcome: Playable APK produced (GDDW_007.apk); source documentation on GitHub

# Discussion

The experiments reveal a clear bifurcation in LLM utility for Android game development:

- **Strengths of direct generation** — Excellent for isolated, well-scoped utility apps or initial prototypes
- **Catastrophic weaknesses in iterative, stateful development** — Context window saturation leads to repetitive behavior, timeout cascades, and irrecoverable project states
- **Texture and rendering limitations** — Consistent refusal or poor handling of dynamic/procedural assets beyond trivial cases
- **Prompt engineering as force multiplier** — Using one LLM (especially Grok) to architect a clean, comprehensive framework prompt dramatically outperforms direct long-context iteration with Gemini

These findings align with broader observations in LLM research: performance degrades sharply with increasing conversational length and task complexity due to attention dilution and compounding errors in self-referential modifications.

# Conclusion

Direct use of Gemini in Android Studio enables rapid creation of simple Android applications but proves unreliable for evolving complex mobile games through iterative prompting. The most effective strategy observed is a **two-stage, cross-model pipeline**:

1. Leverage a strong reasoning model (e.g., Grok) to design a detailed, self-contained framework prompt.
2. Apply that prompt in a fresh IDE session with Gemini for code realization.

This "AI as middleman" approach mitigates context collapse and assumption drift, producing playable results where direct methods fail. Future work could quantify context-length thresholds, compare additional models (e.g., Claude, Llama variants), or integrate retrieval-augmented generation to preserve critical project state.

The experiments provide valuable practitioner evidence that, as of early 2026, effective AI-assisted mobile game development still requires significant human oversight in prompt design and error recovery, rather than fully autonomous code evolution. APKs and documentation are publicly available for replication and extension.
