# Local Model Integration: Nanobrowser

## Overview
Nanobrowser supports using local models through Ollama and other OpenAI-compatible providers. This allows users to run models on their own hardware, eliminating API costs and enhancing privacy by keeping all data on their own machine.

## Supported Local Model Providers

### Ollama
Ollama is the primary supported local model provider, offering easy setup and a compatible API for running various language models locally.

#### Setup Process
1. Install Ollama from [ollama.ai](https://ollama.ai)
2. Pull one of the recommended models:
   ```bash
   ollama pull qwen3:14b
   # or
   ollama pull falcon3:10b
   # or
   ollama pull qwen:2.5-coder-14b
   # or
   ollama pull mistral-small:24b
   ```
3. Start the Ollama service
4. In Nanobrowser settings, select "Ollama" as the provider and configure the endpoint (typically http://localhost:11434)

### Custom OpenAI-Compatible Providers
Nanobrowser also supports any provider that offers an OpenAI-compatible API, such as:
- LocalAI
- LM Studio
- Jan
- Serge

#### Setup Process
1. Install and configure the chosen provider
2. Ensure it's running with an OpenAI-compatible API endpoint
3. In Nanobrowser settings, select "Custom OpenAI-compatible API" and enter the endpoint URL

## Recommended Models

### Performance Tiers

#### High Performance (Larger Models)
- **Mistral Small 24B**: Excellent general reasoning and navigation
- **Qwen 3 14B**: Strong performance across planning and navigation tasks
- **Qwen 2.5 Coder 14B**: Particularly good at understanding web structures

#### Balanced (Medium-Sized Models)
- **Falcon 3 10B**: Good balance of performance and resource requirements
- **Mistral 7B Instruct**: Efficient for basic navigation tasks
- **Llama 3 8B Instruct**: Works well for simpler web interactions

#### Lightweight (Smaller Models)
- **Phi-3 3B**: Minimal resource requirements, suitable for basic tasks
- **Gemma 2B Instruct**: Very lightweight with acceptable performance on simple websites

## Hardware Requirements

### Minimum Requirements
- 8GB RAM
- Modern CPU with 4+ cores
- 10GB free disk space

### Recommended Requirements
- 16GB+ RAM
- Modern CPU with 8+ cores
- GPU with 8GB+ VRAM (significantly improves performance)
- 50GB+ free disk space for multiple models

## Optimizing Local Model Performance

### Prompt Engineering Tips
Local models require more specific and cleaner prompts than cloud APIs:
- Break complex tasks into clear, detailed steps
- Provide explicit context and constraints
- Avoid high-level, ambiguous commands
- Use specific element identifiers when possible

### Model Configuration
- **Temperature**: Lower settings (0.1-0.3) work better for structured tasks
- **Context Window**: Use the maximum available for your hardware
- **System Prompts**: More detailed system prompts often improve performance

## Limitations and Considerations
- Local models typically perform less consistently than cloud APIs
- Resource-intensive models may slow down other applications
- Complex websites may challenge smaller models
- Task completion may require more steps and iterations
- GPU acceleration is strongly recommended for larger models

## Troubleshooting
- If a model is unresponsive, check the Ollama/provider logs
- For out-of-memory errors, try a smaller model or increase swap space
- If actions fail, try breaking tasks into smaller steps
- For slow performance, ensure GPU acceleration is properly configured
- When models produce invalid outputs, try reducing the temperature setting
