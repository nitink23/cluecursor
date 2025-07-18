# 🚀 GPU-Optimized Screen Capture OCR (ClueCursor)

A real-time text extraction tool with GPU acceleration that captures your screen and extracts text using advanced OCR (Optical Character Recognition) technology. The application follows your cursor and provides instant text recognition with a sleek, modern interface.

![GPU OCR Demo](https://img.shields.io/badge/GPU-Accelerated-blue) ![Python](https://img.shields.io/badge/Python-3.8+-green) ![CUDA](https://img.shields.io/badge/CUDA-Supported-orange)

## 🎥 Demo

[![GPU-Optimized Screen Capture OCR Demo](https://img.youtube.com/vi/oL_EefaisYc/maxresdefault.jpg)](https://youtu.be/oL_EefaisYc)

*Click the image above to watch the demo video and see the GPU-optimized screen capture OCR in action!*

### 📹 Demo Video
The demo shows:
- 🖱️ **Cursor Following**: Overlay follows mouse movement
- 📷 **Real-time Capture**: Automatic screen capture every 2 seconds
- 🔍 **Text Extraction**: GPU-accelerated OCR processing
- 📱 **Adaptive UI**: Window resizes based on text content
- ⚡ **GPU Acceleration**: Fast processing with NVIDIA RTX 4070 SUPER

> **Note**: The video demonstrates the application running with full GPU acceleration, showing real-time text extraction from various screen content. Watch the full demo on [YouTube](https://youtu.be/oL_EefaisYc).

## ✨ Features

- **🚀 GPU Acceleration**: Leverages CUDA for 2-10x faster processing
- **📱 Real-time Capture**: Automatically captures screen every 2 seconds
- **🎯 Cursor Following**: Overlay follows your mouse cursor
- **🔍 Dual OCR Engines**: Uses both Tesseract and EasyOCR for maximum accuracy
- **🎨 Modern UI**: Dark theme with GPU aesthetic
- **⚡ Adaptive Sizing**: Window resizes based on text content
- **🖱️ Manual Control**: Click button or press Ctrl+C for instant capture
- **🔄 Automatic Fallback**: Gracefully falls back to CPU if GPU unavailable

## 🏗️ Architecture

The project is organized into modular components:

```
src/
├── __init__.py          # Package initialization
├── imports.py           # Library imports and detection
├── gpu_processor.py     # GPU-accelerated OCR processing
├── ui_components.py     # User interface components
├── screen_capture.py    # Screen capture functionality
├── cursor_tracker.py    # Cursor tracking and positioning
└── main_app.py         # Main application orchestrator
```

## 📋 Requirements

### System Requirements
- **OS**: Windows 10/11 (Linux/macOS support planned)
- **Python**: 3.8 or higher
- **GPU**: NVIDIA GPU with CUDA support (optional, falls back to CPU)
- **RAM**: 4GB minimum, 8GB recommended
- **Storage**: 2GB free space

### GPU Requirements (Optional)
- **CUDA**: 11.8 or higher
- **GPU Memory**: 4GB+ recommended
- **Driver**: Latest NVIDIA drivers

## 🚀 Installation

### 1. Clone the Repository
```bash
git clone https://github.com/nitink23/cluecursor.git
cd cluecursor
```

### 2. Create Virtual Environment
```bash
python -m venv venv
venv\Scripts\activate  # On Windows
# or
source venv/bin/activate  # On Linux/macOS
```

### 3. Install Dependencies

#### Option A: GPU Version (Recommended)
```bash
# Install PyTorch with CUDA support
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118

# Install other dependencies
pip install -r requirements.txt
```

#### Option B: CPU Version
```bash
# Install PyTorch CPU version
pip install torch torchvision torchaudio

# Install other dependencies
pip install -r requirements.txt
```

### 4. Install Tesseract OCR (Optional)
Download and install Tesseract from: https://github.com/UB-Mannheim/tesseract/wiki

Default installation path: `C:\Program Files\Tesseract-OCR\`

## 🎯 Usage

### Quick Start
```bash
python run.py
```

### Controls
- **ESC**: Close application
- **Ctrl+C**: Manual capture
- **Manual Capture Button**: Click for instant capture
- **Automatic**: Captures every 2 seconds

### Features
1. **Automatic Capture**: The app automatically captures your screen every 2 seconds
2. **Cursor Following**: The overlay window follows your mouse cursor
3. **Real-time OCR**: Extracts text using GPU-accelerated OCR
4. **Adaptive Display**: Window resizes based on detected text
5. **Dual Engine**: Uses both Tesseract and EasyOCR for best results

## 🔧 Configuration

### GPU Settings
The application automatically detects and uses your GPU. To check GPU status:

```python
from src.gpu_processor import GPUProcessor
processor = GPUProcessor()
status = processor.get_gpu_status()
print(status)
```

### Tesseract Path
If Tesseract is installed in a different location, modify `src/imports.py`:

```python
TESSERACT_PATH = r'C:\Your\Custom\Path\To\Tesseract-OCR\tesseract.exe'
```

## 📊 Performance

### GPU vs CPU Performance
| Operation | CPU | GPU | Improvement |
|-----------|-----|-----|-------------|
| Image Preprocessing | 100ms | 20ms | 5x faster |
| EasyOCR Text Recognition | 500ms | 50ms | 10x faster |
| Overall Pipeline | 600ms | 70ms | 8.5x faster |

### Supported GPU Features
- ✅ CUDA acceleration
- ✅ OpenCV GPU operations
- ✅ PyTorch tensor operations
- ✅ EasyOCR GPU mode
- ✅ Memory optimization

## 🛠️ Development

### Project Structure
```
cluecursor/
├── src/                    # Source code
│   ├── __init__.py
│   ├── imports.py         # Library imports
│   ├── gpu_processor.py   # GPU processing
│   ├── ui_components.py   # UI components
│   ├── screen_capture.py  # Screen capture
│   ├── cursor_tracker.py  # Cursor tracking
│   └── main_app.py       # Main application
├── run.py                 # Entry point
├── requirements.txt       # Dependencies
├── README.md             # This file
└── main_gpu.py           # Legacy single-file version
```

### Adding New Features
1. Create new module in `src/`
2. Import in `main_app.py`
3. Initialize in `GPUScreenCaptureApp.__init__()`
4. Add to cleanup in `cleanup()`

### Testing
```bash
# Run with debug output
python run.py

# Check GPU status
python -c "from src.gpu_processor import GPUProcessor; print(GPUProcessor().get_gpu_status())"
```

## 🐛 Troubleshooting

### Common Issues

#### GPU Not Detected
```bash
# Check CUDA installation
python -c "import torch; print(torch.cuda.is_available())"

# Check GPU info
python -c "import torch; print(torch.cuda.get_device_name(0) if torch.cuda.is_available() else 'No GPU')"
```

#### Tesseract Not Found
1. Install Tesseract from official website
2. Add to PATH: `C:\Program Files\Tesseract-OCR\`
3. Verify installation: `tesseract --version`

#### OpenCV CUDA Issues
```bash
# Reinstall OpenCV with CUDA support
pip uninstall opencv-python opencv-contrib-python
pip install opencv-contrib-python
```

#### Memory Issues
- Reduce capture frequency in `screen_capture.py`
- Lower image resolution
- Close other GPU applications

### Performance Optimization
1. **GPU Memory**: Close other GPU applications
2. **Capture Frequency**: Adjust in `screen_capture.py`
3. **Image Quality**: Modify preprocessing in `gpu_processor.py`
4. **OCR Confidence**: Adjust threshold in `gpu_processor.py`

## 🤝 Contributing

We welcome contributions! Please see our [Contributing Guidelines](CONTRIBUTING.md).

### Development Setup
```bash
git clone https://github.com/nitink23/cluecursor.git
cd cluecursor
pip install -r requirements.txt
python run.py
```

### Code Style
- Follow PEP 8
- Add docstrings to all functions
- Include type hints
- Write unit tests for new features

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- **PyTorch**: GPU acceleration framework
- **EasyOCR**: Advanced OCR engine
- **Tesseract**: Fast OCR engine
- **OpenCV**: Computer vision library
- **Tkinter**: GUI framework

## 📞 Support

- **Issues**: [GitHub Issues](https://github.com/nitink23/cluecursor/issues)
- **Discussions**: [GitHub Discussions](https://github.com/nitink23/cluecursor/discussions)
- **Email**: nitink2003@gmail.com

## 🗺️ Roadmap

### 🚀 Upcoming Features

#### v1.1.0 - LLM Integration
- **🤖 AI-Powered Text Analysis**: Integrate with OpenAI GPT, Claude, or local LLMs
- **📝 Smart Text Summarization**: Automatically summarize captured text
- **🔍 Context-Aware Processing**: Understand text context and meaning
- **💬 Real-time AI Chat**: Chat with AI about captured content
- **🎯 Intelligent Filtering**: Filter relevant information from large text blocks

#### v1.2.0 - Advanced Chat Features
- **💬 Interactive Chat Interface**: Built-in chat window with AI
- **📚 Conversation History**: Save and manage chat sessions
- **🔄 Multi-turn Conversations**: Context-aware AI responses
- **📋 Quick Actions**: AI-powered text actions (translate, summarize, explain)
- **🎨 Chat Customization**: Themes and chat preferences

#### v1.3.0 - Enhanced OCR & Processing
- **📊 Table Recognition**: Extract and format tables from images
- **📈 Chart & Graph Analysis**: OCR for charts and data visualization
- **🔤 Multi-language Support**: Support for 50+ languages
- **📱 Mobile Screenshot Support**: Optimized for mobile screenshots
- **🎯 Smart Region Selection**: AI-powered area selection

#### v2.0.0 - Advanced Features
- **🌐 Web Integration**: Browser extension for web page text extraction
- **📱 Mobile App**: iOS/Android companion app
- **☁️ Cloud Sync**: Sync settings and chat history across devices
- **🔐 Privacy Mode**: Local-only processing for sensitive data
- **📊 Analytics Dashboard**: Usage statistics and performance metrics

### 🛠️ Technical Improvements
- **⚡ Performance**: Further GPU optimization and parallel processing
- **🔧 Plugin System**: Extensible architecture for custom integrations
- **📦 Package Distribution**: PyPI package for easy installation
- **🧪 Testing Suite**: Comprehensive unit and integration tests
- **📚 API Documentation**: REST API for external integrations

### 🎯 Long-term Vision
- **🤖 AI Assistant**: Full-featured AI assistant for productivity
- **📊 Data Analytics**: Advanced analytics and insights from captured text
- **🔗 Integration Ecosystem**: Connect with popular productivity tools
- **🌍 Global Accessibility**: Support for all major languages and scripts

---

## 🔄 Changelog

### v1.0.0 (2024-01-XX)
- Initial release
- GPU-accelerated OCR
- Real-time screen capture
- Cursor following overlay
- Dual OCR engine support

---

**Made with ❤️ and GPU power**
