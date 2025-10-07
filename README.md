# AI-Content-Velocity-Agent-N8N: Conversational Scripting

<img width="1533" height="354" alt="{754AEE7C-6DA9-44C4-847F-BFE55969A46F}" src="https://github.com/user-attachments/assets/6446119d-0115-4059-8226-a6d57d5f0e01" />



**The Problem: Scaling High-Quality Voice Content**
Manual content repurposing (Blog → Audio) is slow and expensive, hindering the speed-to-market for valuable thought leadership. Furthermore, relying on unverified content to feed our AI Voice Agents (Revspot's qualification bots) introduces a risk of inconsistent brand voice and script failure.

**The Solution: A Production-Ready AI Agent**
This system is an intelligent, autonomous agent built on n8n that transforms raw text into a high-quality, final audio asset in minutes instead of hours.

**Architecture: Proving Resilience and Reasoning**
The workflow is designed as a multi-stage Agent Orchestration Pipeline, where each step provides a technical guardrail:

| **Component**                     | **Node Used**                | **Technical Function & Logic**                                                                                                             
|-----------------------------------|-----------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------
| **Triage Agent (Reasoning)**      | Mistral LLM + IF Node        | **Guardrail:** Auto-verifies content readiness. If the input is **< 250 words** or contains **"DRAFT"**, the job is **REJECTED** (preventing unnecessary API costs).                                                         
| **Data Cleansing**                | Edit Fields (Set)            | Robustness: Cleans the LLM output using JavaScript methods to strip line breaks, smart quotes, and hidden characters—ensuring the string is pure **ASCII** for the external API.                                    
| **Editor Agent (Transformation)** | Mistral LLM                  | Persona Prompting Rewrites the text with a System Role of Professional Podcast Host to ensure the tone is conversational and engaging.                                |
| **Delivery System**               | ElevenLabs, Google Drive     | **Persistence & Accountability:** Generates the **audio** and orchestrates the **upload to Google Drive**, ensuring the final public **Audio URL** is written back to the source spreadsheet (closing the feedback loop).     


**Tools used and their purpose**:

| **Category**             | **Tool**                     | **Function in the Project**                                                                                                                             
|---------------------------|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------
| **Automation Core**       | n8n (or Make)                | **Workflow Execution Engine (The Manager).** Connects all APIs, manages data flow, and executes conditional logic.                                                                                                         
| **Generative AI (LLM)**   | Mistral AI (via API)         | **Agent Reasoning (The Brain).** Performs the **Triage** (decision-making) and the **Conversational Rewriting** (Editor Agent).                                                                                            
| **Generative AI (Voice)** | 11Labs                       | **Text-to-Speech (TTS) (The Voice).** Generates high-quality, branded MP3 audio from the clean script.                                                                              
| **Data Source / Trigger** | Google Sheets                | **Database/Trigger.** Stores the raw content and the final public URL, initiating the workflow on new row additions.                                                                |
| **Persistence Layer**     | Google Drive                 | **File Storage/Hosting.** Stores the final binary MP3 file and generates the crucial public Audio URL.                                                                               
| **Logic & Cleaning**      | IF Node / Edit Fields (Set)  | **Guardrails.** The IF node executes reasoning. The Edit Fields node uses JavaScript to perform data transformation (stripping quotes & line  breaks).                          


