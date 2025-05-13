# ChatCFD: An AI-Powered CFD Simulation Assistant

ChatCFD is an intelligent CFD agent that helps users run CFD simulations directly from academic papers. Through a conversational chat interface, users can:
- Upload and specify which CFD case from a paper they want to simulate
- Provide the corresponding mesh files for the simulation
- Get step-by-step guidance through the entire simulation process

The system automatically interprets the paper's specifications, configures the OpenFOAM case, and handles the simulation setup, making CFD more accessible to users without extensive domain expertise.

![ChatCFD Overview](figures/chatcfd_overview_4.png)

## Table of Contents
- [ChatCFD: An AI-Powered CFD Simulation Assistant](#chatcfd-an-ai-powered-cfd-simulation-assistant)
  - [Table of Contents](#table-of-contents)
  - [Key Features](#key-features)
  - [System Requirements](#system-requirements)
    - [Core Requirements](#core-requirements)
    - [Python Dependencies Defined in `chatcfd_env.yml`](#python-dependencies-defined-in-chatcfd_envyml)
    - [Operating System](#operating-system)
  - [Installation](#installation)
    - [Step 1: Environment Setup](#step-1-environment-setup)
    - [Step 2: Configuration](#step-2-configuration)
    - [Step 3: Launch the Interface](#step-3-launch-the-interface)
  - [Architecture](#architecture)
  - [Usage](#usage)
  - [Performance](#performance)
  - [Support](#support)
  - [License](#license)
  - [Citation](#citation)

## Key Features

- 🤖 **Interactive Multimodal Interface**: Supports PDF papers, mesh files, and natural language dialogue through a ChatGPT-like interface
- 🧠 **Intelligent Case Configuration**: Automatically configures OpenFOAM cases based on academic literature
- 🤝 **Multi-Agent Architecture**: Utilizes specialized AI agents with Retrieval-Augmented Generation (RAG)
- 🔧 **Robust Error Correction**: Implements a multi-category error correction system for enhanced simulation reliability
- 🔄 **OpenFOAM Integration**: Seamlessly works with OpenFOAM framework for CFD simulations

## System Requirements

### Core Requirements
- Python 3.11.4 or higher
- OpenFOAM v2406 installation
- CUDA-capable GPU (optional, but recommended for better performance)

### Python Dependencies Defined in `chatcfd_env.yml`
- **Machine Learning & AI**:
  - PyTorch 2.6.0
  - Transformers 4.50.3
  - Sentence-Transformers 4.0.1
  - FAISS-CPU 1.7.4 (for vector similarity search)
  - Scikit-learn 1.6.1
  - NumPy 1.26.4
  - Pandas 2.2.3

- **Web & API**:
  - Streamlit 1.41.1 (for web interface)
  - OpenAI 1.39.0
  - LangChain 0.1.19
  - FastAPI and related dependencies

- **PDF Processing**:
  - PDFPlumber 0.11.5
  - PyPDF2 3.0.1
  - PDFMiner.six 20231228

- **OpenFOAM Integration**:
  - PyFoam 2023.7

### Operating System
- Linux (recommended for OpenFOAM compatibility)
- Windows with WSL2 (Windows Subsystem for Linux)

## Installation

### Step 1: Environment Setup

1. Create the conda environment:
```bash
conda env create -f chatcfd_env.yml
```

2. Activate the environment:
```bash
conda activate chatcfd
```

3. Verify key components:
```bash
# Test FAISS installation
python -c "import faiss; print(faiss.IndexFlatL2(10))"

# Test PyFoam installation
python -c "from PyFoam.RunDictionary.ParsedParameterFile import ParsedParameterFile; print('PyFoam OK')"
```

4. Download and verify `SentenceTransformer`:
```bash
# Download the model
python test_env/download_model.py

# Test the model
python test_env/test_all_mpnet_base_v2.py
```

Expected output (CPU):
```
GPU Available: False
GPU Name: None
Similarity 0-1: 0.383
Similarity 0-2: 0.182
```

Note: Results will differ if using GPU.

### Step 2: Configuration

Configure the system by editing `inputs/chatcfd_config.json`:
   - Set your API keys, urls, and model names for `DeepSeek` models
   - Configure OpenFOAM paths
   - Adjust other parameters as needed

### Step 3: Launch the Interface

Start the ChatCFD interface:
```bash
streamlit run src/chatbot.py
```

The interface should look similar to:
![ChatCFD Interface](figures/user_interface_demo.png)

Then the user should upload the pdf file, specify the CFD case, and upload the CFD mesh file following the guidance of ChatCFD.

## Architecture

![ChatCFD Architecture](figures/chatcfd_framework_4.png)

ChatCFD implements a comprehensive five-stage workflow to automate CFD simulations:

1. **Interacting** 🗣️
   - Intuitive interface for uploading papers and mesh files
   - Natural language interaction for case specification
   - Guided user experience for simulation setup

2. **Processing data** 📊
   - Systematic analysis of OpenFOAM tutorial cases
   - Structured knowledge base construction
   - Parameter cataloging (solvers, turbulence models, dependencies)

3. **Initiating case files** ⚙️
   - Automated configuration file generation
   - Research paper analysis for parameter extraction
   - Comprehensive case setup based on publication specifications

4. **Running the case** 🚀
   - Mesh file conversion to OpenFOAM format
   - Optimized solver execution
   - Real-time monitoring and logging

5. **Correcting case files** 🔧
   - Intelligent error detection and management
   - Four-category error handling:
     - Dimensional inconsistencies
     - Missing configurations
     - Persistent errors
     - Common setup issues
   - Dual retrieval system for error resolution
   - Iterative refinement (up to 30 iterations)

The system employs a reflection mechanism between execution and correction stages, ensuring robust error handling while maintaining computational efficiency.

## Usage

1. 📄 **Upload Documents**: Start by uploading relevant academic papers in PDF format
2. 📦 **Provide Mesh**: Upload your mesh files (supported formats: OpenFOAM, Fluent)
3. 💬 **Interactive Configuration**: Use natural language to describe your simulation requirements
4. ⚙️ **Case Execution**: Let ChatCFD handle the case setup and execution
5. 🔍 **Error Handling**: The system will automatically detect and correct common errors

## Performance

ChatCFD has demonstrated:
- 📊 30-40% success rate in direct case configuration from literature
- 🎯 60-80% operational success rate for incompressible and compressible CFD cases
- 🛡️ Robust error handling and correction capabilities

## Support

For detailed usage instructions and support, please refer to the documentation or contact the development team.

## License

[Add license information here]

## Citation

[Add citation information here]