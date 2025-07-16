# Fetching Uniswap V2 Tokens: Step-by-Step Guide

## 1. Setting Up the Environment

### Prerequisites
- Node.js and npm/yarn
- TypeScript configured in your project
- Access to an Ethereum RPC endpoint (Sepolia)
- A deployed subgraph on The Graph Studio

### Environment Variables
Create a `.env` file with the following variables:
- GRAPHQL_API_KEY: Your Graph API key
- ETH_RPC_URL: Your Sepolia RPC URL
- DATABASE_URL: MongoDB connection string (if using database storage)