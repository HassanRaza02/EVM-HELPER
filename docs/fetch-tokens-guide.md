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

## 3. Validating Token Contracts

### Basic Security Checks
For each token, perform these validations:
1. Contract exists and is accessible
2. Has valid name and symbol properties
3. Has non-zero total supply
4. Implements standard ERC20 functions

## 4. Processing Token Data

### Token Data Structure
For each valid token, create a structured object with:
- Basic information (address, symbol, name)
- Liquidity and reserve data
- Network identifier (e.g., "sepolia")
- Validation timestamp and status

### Processing Steps
1. Extract token data from pair information
2. Format and normalize data (e.g., convert wei to ether)
3. Add metadata like network identifier
4. Validate tokens using security checks
5. Filter out invalid tokens (with exceptions for essential tokens like WETH)

## 5. Storage Options

### In-Memory Storage
- Store tokens in arrays or maps
- Suitable for simple scripts or one-time runs
- No persistence between script executions

### File-Based Storage
- Save tokens to JSON files
- Simple persistence without database setup
- Easy to version control and share

### Database Storage (MongoDB)
- Define schema and model for tokens
- Implement CRUD operations
- Support for querying and indexing
- Suitable for production applications

## 6. Scheduling Regular Updates

### Using node-cron
- Set up a schedule (e.g., every 5 minutes)
- Implement the job function to fetch and process tokens
- Handle job completion and error cases

### Preventing Overlapping Jobs
- Use a flag to track if a job is running
- Skip new job execution if previous job is still running
- Reset flag when job completes or fails
- Log job status for monitoring


## 7. Handling Token Prices

### Calculating Prices from Reserves
- For tokens paired with ETH, calculate price from reserves
- Account for token decimals in calculations
- Format prices in ETH and USD terms

### Using derivedETH from Subgraph
- Query token.derivedETH values if available
- Fetch ETH price in USD
- Calculate USD price by multiplying derivedETH by ETH price