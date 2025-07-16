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

### Required Dependencies
- graphql-request: For querying The Graph API
- dotenv: For loading environment variables
- ethers: For interacting with Ethereum contracts
- axios: For making HTTP requests
- mongoose: For database operations (optional)
- node-cron: For scheduling jobs (optional)

## 2. Fetching Token Pairs from the Subgraph

### GraphQL Query Structure
Create a GraphQL query that fetches:
- Pair addresses and creation timestamps
- Token addresses, symbols, and names
- Reserves and liquidity information

### Key Query Parameters
- Limit results to a manageable number (e.g., 50 pairs)
- Order by creation time (newest first)
- Filter for pairs with non-zero reserves

### Implementation Steps
1. Set up the GraphQL endpoint with your API key
2. Create the query structure to fetch required data
3. Handle authentication with The Graph API
4. Process and log the response data