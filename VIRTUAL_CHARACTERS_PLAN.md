# Virtual Character Douyin – Implementation Plan

This document outlines a high level plan for extending the existing Douyin-Vue project. Instead of showing user-uploaded videos, each slide will present an AI-driven virtual character. Users can talk with these characters through speech.

## Core Idea
- Every time the user swipes to a new page, a new virtual character is generated.
- Characters have different professions, skills, images and backgrounds. Images are produced via an image generation service.
- Users speak into the microphone. Their speech is converted to text using a Speech-to-Text (STT) API.
- The text is sent to a language model backend along with the character’s profile to generate a response.
- The response text is transformed to audio by a Text-to-Speech (TTS) API and played back to the user.
- The app records how long the user stays on each character. Future characters are generated to better match user preferences.

## Key Components To Modify
1. **Home Slide Feed**
   - Replace video items with virtual character components that display a generated avatar/background.
   - Each slide should include a microphone button for capturing speech and a play button for TTS playback.

2. **Stores & State Management**
   - Add a Pinia store to track generated characters, user dwell time, and preference data.
   - Provide actions for requesting new character profiles and storing usage metrics.

3. **API Modules**
   - Create wrapper functions for STT, language model, TTS, and image generation services.
   - These functions will be used by the new store and components.

4. **UI Components**
   - Develop a `VirtualCharacter.vue` component to handle the image, chat history display, STT recording control, and audio playback.
   - Update router or slide logic so each swipe instantiates a new character using the store and API modules.

5. **Recommendation Logic**
   - Track time spent on each character in the store.
   - Implement a simple algorithm that favors character attributes which the user lingers on the most.
   - This can be refined over time into a more advanced model.

6. **Additional Considerations**
   - Ensure asynchronous API calls are handled smoothly to keep swiping/interaction responsive.
   - Cache generated avatars or responses where possible to reduce API usage.

This plan provides the starting direction to transform the current TikTok-like video feed into an interactive feed of AI-generated virtual characters.
