# local-LLM
local-LLM: A powerful, locally-hosted AI chat interface
# Claude-Style Local Chat

A powerful, locally-hosted AI chat interface optimized for NVIDIA RTX 5070Ti and AMD Ryzen 9 7950X.

![Claude-Style Chat Interface](screenshots/interface.png)

## 🚀 Features

- **Multiple Model Support**: Run Llama 2 70B, Mistral 7B, Yi 34B, and more
- **Streaming Responses**: Real-time text generation
- **Claude-like UI**: Clean, modern interface
- **Hardware Optimized**: Specifically tuned for RTX 5070Ti (16GB VRAM)
- **4-bit Quantization**: Run large models efficiently
- **Conversation Management**: Save and load chat histories
- **System Monitoring**: Real-time GPU/CPU usage tracking

## 📋 Requirements

### Hardware
- NVIDIA RTX 5070Ti (16GB VRAM) or similar
- 32GB+ System RAM
- 100GB+ Storage space for models

### Software
- Ubuntu 24.04 LTS or Windows 11 with WSL2
- Python 3.10+
- CUDA 12.8+
- NVIDIA Driver 535+

## 🛠️ Installation

### 1. Clone the Repository
```bash
git clone https://github.com/prashanthag/local-LLM.git
cd claude-chat
```

### 2. Run Automated Setup
```bash
chmod +x setup.sh
./setup.sh
```

This will:
- Install system dependencies
- Create Python virtual environment
- Install required packages
- Configure CUDA support
- Test the setup

### 3. Download Models
```bash
# Activate virtual environment
source venv/bin/activate

# Download models (this will take 30-60 minutes)
python download_models.py
```

### 4. Run the Application
```bash
python app.py
```

Access the interface at `http://localhost:7860`

## 📱 Usage

### Basic Chat
1. Type your message in the text box
2. Press Enter or click "Send"
3. Watch as the AI generates a response in real-time

### Model Switching
1. Use the dropdown in the right panel to select different models
2. Each model has different capabilities:
   - **Mistral 7B**: Fast, general-purpose
   - **Llama 2 70B**: Most capable, slower
   - **Yi 34B**: Good balance of speed and quality

### Advanced Settings
- **Temperature**: Controls randomness (0.1 = focused, 2.0 = creative)
- **Max Tokens**: Maximum response length
- **System Prompt**: Customize the AI's behavior

## 🔧 Configuration

### Hardware Optimization

Edit `hardware_config.py` to tune for your specific hardware:

```python
# For different GPU configurations
MODEL_CONFIGS = {
    "llama-70b": {
        "max_memory": {0: "15GB", "cpu": "30GB"},  # Adjust based on your VRAM
        "quantization": {
            "load_in_4bit": True,  # Use 8-bit for better quality if you have more VRAM
        }
    }
}
```

### Adding New Models

Add a new model configuration in `hardware_config.py`:

```python
MODEL_CONFIGS["new-model"] = {
    "model_id": "org/model-name",
    "quantization": {
        "load_in_4bit": True,
    },
    "device_map": "auto",
}
```

## 🐳 Docker Deployment

```bash
# Build the image
docker build -t claude-chat .

# Run the container
docker run --gpus all -p 7860:7860 claude-chat
```

## 📊 Performance Optimization

### Memory Management
- The app automatically manages GPU memory
- Models are loaded with 4-bit quantization
- CPU offloading is used for large models

### Speed Optimization
- Flash Attention 2 is enabled when available
- Batch processing for multiple requests
- Optimized thread configuration for AMD Ryzen

## 🔍 Troubleshooting

### Common Issues

1. **CUDA not available**
   ```bash
   # Check NVIDIA driver
   nvidia-smi
   
   # Reinstall CUDA toolkit
   sudo apt install nvidia-cuda-toolkit
   ```

2. **Out of Memory**
   - Reduce batch size in configuration
   - Use more aggressive quantization
   - Close other GPU applications

3. **Slow Generation**
   - Enable Flash Attention
   - Reduce max_tokens
   - Use smaller models

### Logs
```bash
# View application logs
tail -f logs/app.log

# Check GPU usage
nvidia-smi -l 1
```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Submit a pull request

## 📄 License

MIT License - see LICENSE file for details

## 🙏 Acknowledgments

- Hugging Face for Transformers library
- Meta for Llama 2
- Mistral AI for Mistral models
- Gradio team for the UI framework

## 📞 Support

- GitHub Issues: [Report a bug](https://github.com/yourusername/claude-chat/issues)
- Documentation: [Wiki](https://github.com/yourusername/claude-chat/wiki)

---

Built with ❤️ for the open-source AI community
