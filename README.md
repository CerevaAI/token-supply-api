# Tokenomics Supply API

A Node.js based REST API service for querying token supply data. The service reads tokenomics data in CSV format and provides an interface to query token supply by category based on timestamps.

## Features

- Parse and read tokenomics CSV data
- Query supply by timestamp
- Return total supply, circulating supply, and detailed category breakdowns
- RESTful API design
- Caching for DAO reserve supply

## Installation

Requires Node.js (v14+). To install:

```bash
# Clone repository
git clone [repository-url]

# Install dependencies
cd [project-directory]
npm install
```

## Configuration

### Environment Variables

The following environment variables can be configured:

- `PORT`: The port on which the server will run (default: 3000)
- `CSV_FILE_PATH`: Path to the tokenomics CSV file (default: `./data/tokenomics.csv`)

### CSV Data Format Requirements

The tokenomics.csv file should contain these columns:

- Date: Release date (YYYY/MM/DD)
- Month: Month number
- Booster Event: Booster allocation
- Initial Liquidity & MM Fund: Initial liquidity
- Private Sale: Private sale allocation
- Public Sale: Public sale allocation
- KOL Round: KOL round allocation
- Marketing: Marketing allocation
- Ecosystem Fund: Ecosystem fund allocation
- Community: Community allocation
- Total: Total supply

## Usage

```bash
# Start server
npm start
```

Server will run at http://localhost:3000

### API Endpoints

#### GET /

Query token supply data for a specific timestamp.

**Parameters:**

- timestamp (optional): ISO format timestamp, defaults to current time

**Example Requests:**

```bash
# Query current supply
curl http://localhost:3000/

# Query supply for specific time
curl http://localhost:3000/?timestamp=2024-08-23T00:00:00Z
```

**Response Format:**

```json
{
  "timestamp": "2024-08-23T00:00:00Z",
  "timeRange": "2024/08/22 - 2024/08/23 (Current: 2024/08/23)",
  "maxSupply": 2000000000,
  "totalSupply": 1772916667,
  "circulatingSupply": 1500000000,
  "daoReserveSupply": 272916667,
  "circulatingPercent": 0.75,
  "categorySupply": {
    "boosterEvent": 1000000000,
    "liquidityAndMMFund": 300000000,
    "privateSale": 29166666.67,
    "publicSale": 225000000,
    "kolRound": 31250000,
    "marketing": 41666666.67,
    "ecosystemFund": 104166666.67,
    "community": 41666666.67
  },
  "csv": "https://github.com/Cereva/token-supply-api/blob/main/tokenomics.csv"
}
```

#### GET /circulatingSupply

Query circulating supply data for a specific timestamp.

**Parameters:**

- timestamp (optional): ISO format timestamp, defaults to current time

**Example Requests:**

```bash
# Query current circulating supply
curl http://localhost:3000/circulatingSupply

# Query circulating supply for specific time
curl http://localhost:3000/circulatingSupply?timestamp=2024-08-23T00:00:00Z
```

**Response Format:**

```json
1500000000
```

#### GET /circulatingSupply/json

Query circulating supply data for a specific timestamp and return as JSON.

**Parameters:**

- timestamp (optional): ISO format timestamp, defaults to current time

**Example Requests:**

```bash
# Query current circulating supply
curl http://localhost:3000/circulatingSupply/json

# Query circulating supply for specific time
curl http://localhost:3000/circulatingSupply/json?timestamp=2024-08-23T00:00:00Z
```

**Response Format:**

```json
{
  "result": 1500000000
}
```

#### GET /totalSupply

Query total supply data for a specific timestamp.

**Parameters:**

- timestamp (optional): ISO format timestamp, defaults to current time

**Example Requests:**

```bash
# Query current total supply
curl http://localhost:3000/totalSupply

# Query total supply for specific time
curl http://localhost:3000/totalSupply?timestamp=2024-08-23T00:00:00Z
```

**Response Format:**

```json
1772916667
```

#### GET /totalSupply/json

Query total supply data for a specific timestamp and return as JSON.

**Parameters:**

- timestamp (optional): ISO format timestamp, defaults to current time

**Example Requests:**

```bash
# Query current total supply
curl http://localhost:3000/totalSupply/json

# Query total supply for specific time
curl http://localhost:3000/totalSupply/json?timestamp=2024-08-23T00:00:00Z
```

**Response Format:**

```json
{
  "result": 1772916667
}
```

#### GET /maxSupply

Query max supply data for a specific timestamp.

**Parameters:**

- timestamp (optional): ISO format timestamp, defaults to current time

**Example Requests:**

```bash
# Query current max supply
curl http://localhost:3000/maxSupply

# Query max supply for specific time
curl http://localhost:3000/maxSupply?timestamp=2024-08-23T00:00:00Z
```

**Response Format:**

```json
2000000000
```

#### GET /maxSupply/json

Query max supply data for a specific timestamp and return as JSON.

**Parameters:**

- timestamp (optional): ISO format timestamp, defaults to current time

**Example Requests:**

```bash
# Query current max supply
curl http://localhost:3000/maxSupply/json

# Query max supply for specific time
curl http://localhost:3000/maxSupply/json?timestamp=2024-08-23T00:00:00Z
```

**Response Format:**

```json
{
  "result": 2000000000
}
```

## Dependencies

- express: Web framework
- csv-parser: CSV parsing library
- moment: Date handling library
- web3: Solana JavaScript API

## License

MIT
