# CampusQuest

An intelligent campus information retrieval system powered by Large Language Models (LLM) and generative search capabilities. CampusQuest enables students and staff to query college data in a conversational manner, getting accurate answers about their institution.

## Overview

CampusQuest is a web-based application that combines:
- **LLM-powered Question Answering**: Uses OpenAI's GPT models or Baidu's Ernie for natural language understanding
- **PDF Document Processing**: Extracts and processes college data from PDF documents
- **Vector Database Search**: Uses FAISS and embeddings for semantic search over college information
- **Conversational Interface**: Built with Reflex framework for a responsive UI

## Features

- 🤖 **AI-Powered Chat**: Ask questions about your college in natural language
- 📄 **Document Processing**: Automatically processes college data PDFs
- 🔍 **Semantic Search**: Intelligent retrieval using vector embeddings
- 💬 **Conversation History**: Maintains context across multiple questions
- 🌙 **Dark Mode**: Modern, eye-friendly interface with dark theme support
- 🔄 **Multi-API Support**: Works with both OpenAI and Baidu APIs

## Tech Stack

### Backend
- **Python 3.11**: Core runtime
- **Reflex**: Web framework for building the application
- **LangChain**: LLM orchestration and document processing
- **FAISS**: Vector similarity search
- **OpenAI / Baidu APIs**: Language models

### Frontend
- **Reflex Components**: React-based UI components
- **Chakra UI**: Component library integration
- **Custom CSS Animations**: Enhanced user experience

### Infrastructure
- **Docker**: Containerization for deployment
- **npm**: Frontend dependency management

## Installation

### Prerequisites
- Python 3.11+
- pip
- npm (for frontend dependencies)

### Local Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/blaze22102002/CampusQuest.git
   cd CampusQuest
   ```

2. **Install Python dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Install frontend dependencies**
   ```bash
   npm install
   ```

4. **Set up environment variables**
   ```bash
   cp .env.example .env
   ```
   
   Configure your `.env` file with:
   ```
   OPENAI_API_KEY=your_openai_key
   OPENAI_API_BASE=https://api.openai.com/v1  # Optional
   BAIDU_API_KEY=your_baidu_key  # Optional
   BAIDU_SECRET_KEY=your_baidu_secret  # Optional
   ```

### Docker Setup

Build and run using Docker:

```bash
docker build -t campusquest .
docker run -p 3000:3000 -e OPENAI_API_KEY=your_key campusquest
```

## Usage

### Starting the Application

**Development Mode:**
```bash
reflex run
```

The application will be available at `http://localhost:3000`

**Production Mode:**
```bash
reflex run --env prod
```

### Adding College Data

1. Place your college PDF document in the project root or `webui/` directory
2. Update the file path in `webui/llm.py` (line 38) or `webui/state.py` (line 39)
3. Restart the application

Example:
```python
file_path = "your_college_data.pdf"
loader = PyPDFLoader(file_path)
```

### Querying the System

1. Open the web interface
2. Type your question about the college (e.g., "What are the admission requirements?")
3. The system will search through the college data and provide an answer
4. Continue the conversation with follow-up questions

## Project Structure

```
CampusQuest/
├── webui/                      # Main Reflex application
│   ├── LandingPage.py         # Landing page UI components
│   ├── state.py               # Application state management
│   ├── llm.py                 # LLM configuration and setup
│   ├── styles.py              # CSS styles
│   ├── webui.py               # Main app entry point
│   ├── components/            # Reusable UI components
│   ├── requirements.txt        # Python dependencies for webui
│   └── CLG-DATA-2324.pdf      # Sample college data
├── requirements.txt            # Root Python dependencies
├── rxconfig.py                 # Reflex configuration
├── Dockerfile                  # Docker container definition
├── package.json               # npm configuration
└── .env                       # Environment variables (not committed)
```

## Key Components

### LandingPage.py
Defines the UI landing page with:
- Header with email contact
- Main heading and badges
- Responsive design for desktop and mobile

### state.py
Manages application state including:
- Chat conversations
- Question processing
- Integration with OpenAI/Baidu APIs
- Document retrieval and answering

### llm.py
Configures the LLM pipeline:
- PDF loading and processing
- Text splitting and chunking
- Vector embeddings using Cohere
- FAISS vector store setup
- Conversational retrieval chain

## API Configuration

### OpenAI
```python
OPENAI_API_KEY=sk-...
llm = ChatOpenAI(model="gpt-3.5-turbo-0125", temperature=0.2)
```

### Baidu (Alternative)
```python
BAIDU_API_KEY=...
BAIDU_SECRET_KEY=...
```

## Vector Search Pipeline

1. **PDF Loading**: Documents are loaded using PyPDFLoader
2. **Text Splitting**: Content is split into chunks (size: 1537, overlap: 200-300)
3. **Embeddings**: Text chunks are converted to vectors using Cohere embeddings
4. **Vector Store**: FAISS stores vectors for fast similarity search
5. **Retrieval**: Relevant chunks are retrieved for each query
6. **Reranking**: Optional Cohere reranking for improved relevance
7. **Generation**: LLM generates answers based on retrieved context

## Dependencies

### Python
- `reflex>=0.2.0` - Web framework
- `openai` - OpenAI API client
- `langchain==0.1.17` - LLM orchestration
- `langchain-cohere==0.1.4` - Cohere embeddings
- `langchain-fireworks==0.1.2` - Fireworks LLM support
- `faiss-cpu==1.8.0` - Vector similarity search
- `pypdf==4.2.0` - PDF processing
- `torch==2.2.2` - ML framework
- `scikit-learn==1.4.1.post1` - ML utilities

### Frontend
See `package.json` for npm dependencies

## Configuration

Edit `rxconfig.py` to modify application settings:
```python
config = rx.Config(
    app_name="webui",
)
```

## Troubleshooting

### PDF Not Found
- Ensure the PDF file path is correct and file exists
- Check file permissions

### API Key Errors
- Verify environment variables are set correctly
- Check API key validity and permissions

### Memory Issues
- Reduce chunk size in text splitter
- Decrease number of retrieved documents (k parameter)

### Slow Responses
- Optimize vector store (use GPU FAISS if available)
- Reduce temperature for faster generation
- Use smaller models

## Docker Deployment

The application includes a Dockerfile for containerized deployment:

```bash
# Build image
docker build -t campusquest:latest .

# Run container
docker run -d \
  -p 3000:3000 \
  -e OPENAI_API_KEY=your_key \
  --name campusquest \
  campusquest:latest
```

## Contributing

Contributions are welcome! Please:
1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## License

This project is open source and available under the MIT License.

## Support

For issues, questions, or suggestions:
- Email: campusquest@gmail.com
- GitHub Issues: [Report a bug](https://github.com/blaze22102002/CampusQuest/issues)

## Future Enhancements

- [ ] Multi-language support
- [ ] Integration with college management systems
- [ ] Advanced analytics dashboard
- [ ] Mobile app
- [ ] Real-time document updates
- [ ] User authentication and personalization
- [ ] Support for multiple document types (HTML, Word, etc.)

## Acknowledgments

- Built with [Reflex](https://reflex.dev/)
- Powered by [LangChain](https://langchain.com/)
- Embeddings by [Cohere](https://cohere.ai/)
- Search by [FAISS](https://github.com/facebookresearch/faiss)
- LLM by [OpenAI](https://openai.com/)

---

**Status**: Active Development  
**Last Updated**: 2026-04-26
