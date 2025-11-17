# Minimum Viable Product (MVP) for Arunika

## 1. Background & Motivation

Arunika brings ordinary **dolls** to life by integrating an AI-powered conversational module during the manufacturing/assembly process. Inspired by Pinocchio’s story, Arunika is a finished product—an interactive talking doll, ready to use out of the box.

**Problem Statement:**  
Most dolls are static and lack meaningful interactivity. "Smart dolls" are limited, locked to proprietary ecosystems, or offer only canned responses. There’s a clear need for an affordable, intelligent companion doll that actually engages and delights children.

## 2. Objectives & Success Metrics

- **Objective:**  
  Deliver a complete, fully-assembled talking doll product (not a DIY device) in partnership with doll manufacturers, powered by Arunika’s conversational AI module.
- **Success Metrics:**  
  - 90%+ user satisfaction (parent/child post-pilot surveys)
  - <2 seconds average response time for doll replies
  - 100+ dolls shipped/sold during pilot launch
  - 80%+ repeat engagement (kids interact >3x/week, via usage logs)
  - At least one signed partnership with a doll factory or character owner

## 3. Target Users

- Parents of children aged 3–10 seeking an interactive, educational, or companion doll experience
- Doll brands/factories aiming to differentiate with smart features

## 4. Core Features

- **Voice Interaction:**  
  Bi-directional speech, optimized for child-doll conversations
- **Conversational AI:**  
  LLM integration (Gemini, OpenAI, etc.) with child-friendly, emotionally intelligent responses
- **Seamless Integration:**  
  Device module pre-installed during factory assembly—no DIY, no installation required for end user
- **Cloud Connectivity:**  
  Secure, reliable WiFi connection to AI services
- **OTA Updates:**  
  Over-the-air firmware/content upgrades, managed by Arunika team

## 5. Technical Approach

- **Manufacturing Partnerships:**  
  Source raw dolls from factory vendors, install Arunika module and casing in-house, assemble finished talking doll product
- **Device Component Sourcing:**  
  ESP32 and related hardware sourced from bulk component suppliers; 3D printed casing produced in bulk
- **Software & Server:**  
  All firmware, cloud integration, and conversational logic developed and maintained by Arunika team
- **Quality Control:**  
  All dolls tested post-assembly for out-of-box functionality and conversational performance
- **Branding:**  
  Minimal at launch (“Powered by Arunika”); future options for character partnerships or licensing

## 6. Non-Functional Requirements

- **Performance:**
  <2s response time for all interactions
- **Reliability:**
  99% cloud uptime for conversational services
- **Scalability:**
  Modular design to support future doll models and feature expansion

## 7. Roadmap & Future Enhancements

### Phase 1: MVP (Launch)
- Core voice interaction with cloud-connected AI
- Conversation logging for analytics and debugging
- OTA firmware updates
- Basic child-friendly responses via Gemini LLM

### Phase 2: Semantic Context Memory (Q2-Q3 2025)
Leveraging ScyllaDB's vector search capabilities to enhance conversational intelligence:

**2.1 Semantic Search for Conversation Context**
- Store embeddings of past user queries and responses
- Search for semantically similar historical conversations when processing new queries
- Use discovered patterns to inform LLM prompts, reducing redundancy and improving response consistency
- **User Benefit:** Doll remembers conversation patterns, provides more coherent and contextual responses

**2.2 Personalized Context Memory**
- Build persistent profiles of each child's interests, learning level, and conversation patterns
- Extract semantic features (topics, complexity preferences, engagement style) from conversation history
- Tailor future responses based on accumulated personal history
- **User Benefit:** Doll becomes more personalized and attuned to each child's unique interests and learning style

### Phase 3: Intelligent Response Optimization (Q3-Q4 2025)
- Identify response patterns that lead to higher engagement and satisfaction
- Store embeddings of successful responses alongside engagement metrics
- Use similarity search to automatically suggest effective response strategies
- **User Benefit:** Continuous improvement of conversation quality without manual prompt tuning

### Phase 4: Advanced Features (2026+)
- Predictive engagement modeling
- Automated prompt optimization based on aggregate user data
- Cross-doll learning (insights from 100+ devices informing better responses for all)
- Integration with parental controls and educational tracking
