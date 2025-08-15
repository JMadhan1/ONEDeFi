
# ONEDeFi - AI-Powered DeFi Assistant

The world's first AI-powered DeFi assistant that acts like your personal financial advisor. Get portfolio health checkups, custom investment strategies, and plain-English explanations of complex DeFi operations across Ethereum, Polygon, and Solana.

## Features

- **Cross-chain Trading**: Execute token swaps across Ethereum, Polygon, and Solana using leading DEX protocols
- **Lending & Borrowing**: Lend assets to earn yield or borrow against collateral using protocols like Aave and Compound
- **Yield Farming**: Provide liquidity to earn trading fees and farm rewards across multiple DeFi protocols
- **AI Portfolio Analysis**: Get intelligent portfolio health checkups and optimization recommendations
- **Multi-chain Support**: Seamless integration with Ethereum, Polygon, and Solana networks

## Supported Blockchains

- **Ethereum**: Uniswap, SushiSwap, Aave, Compound
- **Polygon**: QuickSwap, Aave V3, Curve
- **Solana**: Raydium, Orca, Solend

## Local Development

### Prerequisites

- Python 3.11+
- pip

### Installation

1. Clone the repository:
```bash
git clone <your-repo-url>
cd defimcp
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Set up environment variables:
```bash
# Create a .env file
SESSION_SECRET=your-secret-key
FLASK_DEBUG=True
```

4. Run the application:
```bash
python main.py
```

The application will be available at `http://localhost:5000`

## Deployment on Render

### Automatic Deployment

1. **Connect to Render**: 
   - Go to [Render Dashboard](https://dashboard.render.com)
   - Click "New +" and select "Blueprint"
   - Connect your GitHub repository

2. **Configure Environment**:
   - Render will automatically detect the `render.yaml` configuration
   - The service will be deployed with PostgreSQL database

3. **Environment Variables** (Optional):
   - `SESSION_SECRET`: Secret key for session management (auto-generated)
   - `FLASK_ENV`: Set to "production"
   - `FLASK_DEBUG`: Set to "false"

### Manual Deployment

1. **Create Web Service**:
   - Go to Render Dashboard
   - Click "New +" → "Web Service"
   - Connect your GitHub repository

2. **Configure Service**:
   - **Name**: `onedefi-server`
   - **Environment**: `Python`
   - **Build Command**: `pip install -r requirements.txt`
   - **Start Command**: `gunicorn main:app --bind 0.0.0.0:$PORT`

3. **Create Database**:
   - Go to "New +" → "PostgreSQL"
   - Name: `onedefi-db`
   - Plan: Free

4. **Link Database**:
   - In your web service settings
   - Add environment variable: `DATABASE_URL` → Link to your PostgreSQL database

## Project Structure

```
defimcp/
├── app.py                 # Flask application configuration
├── main.py               # Application entry point
├── models.py             # Database models
├── routes_simple.py      # API routes
├── requirements.txt      # Python dependencies
├── render.yaml          # Render deployment configuration
├── Procfile             # Process file for deployment
├── runtime.txt          # Python version specification
├── .gitignore           # Git ignore rules
├── README.md            # This file
├── blockchain/          # Blockchain integrations
├── config/              # Configuration files
├── defi_tools/          # DeFi operation tools
├── static/              # Static assets (CSS, JS)
├── templates/           # HTML templates
└── utils/               # Utility functions
```

## API Documentation

### Core Endpoints

- `GET /` - Home page
- `GET /dashboard` - User dashboard
- `GET /ai-agent` - AI agent interface
- `GET /api-docs` - API documentation
- `GET /ai-features` - AI features showcase

### Authentication

The application supports OAuth authentication and session-based login.

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

## License

This project is licensed under the MIT License.

## Support

For support and questions, please open an issue in the GitHub repository.

---

**Note**: This is a development version. For production use, ensure proper security configurations and environment variable management.
