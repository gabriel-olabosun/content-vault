# ContentVault

> A revolutionary blockchain-based platform that transforms how communities discover, evaluate, and reward exceptional digital content through collective intelligence.

## Overview

ContentVault creates a self-governing ecosystem where content quality is determined by community consensus rather than algorithmic manipulation. Users contribute valuable links, earn reputation through meaningful participation, and receive direct rewards for quality submissions. The protocol ensures transparency through blockchain immutability while maintaining content standards through community moderation - creating a meritocratic content discovery engine that rewards authentic value creation over engagement gaming.

## Features

### 🔗 Content Submission

- Community-driven content curation system
- Configurable submission fees to prevent spam
- Support for multiple content categories (Technology, Science, Art, Politics, Sports)
- Automatic content validation and storage

### 🗳️ Community Voting

- Binary appraisal system (+1/-1 voting)
- Reputation-based voting with credibility tracking
- Vote history preservation and modification support
- Quality threshold filtering for content visibility

### 💰 Reward System

- Direct STX transfers to content creators
- Transparent reward tracking and history
- Community-driven gratuity distribution
- Incentivizes high-quality content creation

### 🛡️ Content Moderation

- Community-based flagging system
- Administrative content removal capabilities
- Reputation system to encourage quality participation
- Transparent moderation actions

### 📊 Analytics & Queries

- Real-time content ranking and discovery
- User reputation and credibility tracking
- Comprehensive content metadata and statistics
- Top content retrieval with quality filtering

## Smart Contract Architecture

### Core Components

```clarity
;; Main data structures
curated-items          ; Stores all submitted content with metadata
participant-appraisals ; Tracks user votes on content
participant-credibility ; User reputation scores
```

### Key Functions

#### Public Functions

- **`contribute-item`** - Submit new content for community curation
- **`appraise-item`** - Vote on submitted content (+1/-1)
- **`reward-originator`** - Send STX rewards to content creators
- **`flag-item`** - Report problematic content
- **`adjust-submission-charge`** - Admin function to modify submission fees
- **`expunge-item`** - Admin function to remove content
- **`introduce-topic`** - Admin function to add new content categories

#### Read-Only Functions

- **`retrieve-item-details`** - Get complete content information
- **`retrieve-participant-appraisal`** - Check user's vote on content
- **`retrieve-aggregate-submissions`** - Get total submission count
- **`retrieve-participant-credibility`** - Get user reputation score
- **`retrieve-top-items`** - Get highest-rated content

## Getting Started

### Prerequisites

- [Clarinet](https://github.com/hirosystems/clarinet) - Stacks smart contract development tool
- [Node.js](https://nodejs.org/) - For running tests and build scripts
- [Stacks Wallet](https://www.hiro.so/wallet) - For interacting with the contract

### Installation

1. Clone the repository:

```bash
git clone https://github.com/gabriel-olabosun/content-vault.git
cd content-vault
```

2. Install dependencies:

```bash
npm install
```

3. Check contract syntax:

```bash
clarinet check
```

4. Run tests:

```bash
npm test
```

### Development

#### Running Local Development Network

```bash
clarinet integrate
```

#### Contract Deployment

1. **Testnet Deployment:**

```bash
clarinet deploy --testnet
```

2. **Mainnet Deployment:**

```bash
clarinet deploy --mainnet
```

### Usage Examples

#### Submit Content

```clarity
(contract-call? .content-vault contribute-item 
  "Revolutionary Blockchain Article"
  "https://example.com/blockchain-revolution"
  "Technology")
```

#### Vote on Content

```clarity
;; Upvote content (item ID 1)
(contract-call? .content-vault appraise-item u1 1)

;; Downvote content (item ID 1)
(contract-call? .content-vault appraise-item u1 -1)
```

#### Reward Content Creator

```clarity
;; Send 100 microSTX to content creator
(contract-call? .content-vault reward-originator u1 u100)
```

#### Query Content

```clarity
;; Get content details
(contract-call? .content-vault retrieve-item-details u1)

;; Get top 10 content items
(contract-call? .content-vault retrieve-top-items u10)

;; Check user reputation
(contract-call? .content-vault retrieve-participant-credibility 'ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM)
```

## Protocol Parameters

| Parameter | Value | Description |
|-----------|-------|-------------|
| `MIN_HYPERLINK_LENGTH` | 10 | Minimum URL length requirement |
| `submission-charge` | 10 microSTX | Fee for submitting content |
| `MAX_UINT` | 2^128-1 | Maximum integer value |
| Content Topics | 5 default | Technology, Science, Art, Politics, Sports |

## Error Codes

| Code | Constant | Description |
|------|----------|-------------|
| 100 | `ERR_UNAUTHORIZED_ACCESS` | Caller lacks required permissions |
| 101 | `ERR_INVALID_SUBMISSION` | Submission data validation failed |
| 102 | `ERR_DUPLICATE_ENTRY` | Content already exists |
| 103 | `ERR_NONEXISTENT_ITEM` | Referenced content doesn't exist |
| 104 | `ERR_INADEQUATE_BALANCE` | Insufficient STX balance |
| 105 | `ERR_INVALID_TOPIC` | Topic not in allowed list |
| 106 | `ERR_INVALID_FLAG` | Invalid flagging attempt |
| 107 | `ERR_OVERFLOW` | Arithmetic overflow detected |
| 108 | `ERR_INVALID_APPRAISAL` | Vote value not +1 or -1 |
| 109 | `ERR_INVALID_ITEM_ID` | Invalid item identifier |

## Testing

The project includes comprehensive test coverage using Vitest and Clarinet testing framework:

```bash
# Run all tests
npm test

# Run contract validation
clarinet check

# Run specific test file
npm test content-vault.test.ts
```

### Test Coverage

- ✅ Content submission and validation
- ✅ Voting mechanism and reputation tracking
- ✅ Reward distribution system
- ✅ Content flagging and moderation
- ✅ Administrative functions
- ✅ Error handling and edge cases

## Security Considerations

### Access Control

- Administrative functions restricted to `PROTOCOL_ADMINISTRATOR`
- User authorization checks for all state-changing operations
- Balance verification before STX transfers

### Data Integrity

- Overflow protection on arithmetic operations
- Input validation for all user-provided data
- Immutable content storage with transparent modification tracking

### Economic Security

- Submission fees to prevent spam
- Reputation system to incentivize quality participation
- Direct reward mechanism to encourage valuable content

## Roadmap

### Phase 1: Core Protocol ✅

- [x] Basic content submission and voting
- [x] Reputation system implementation
- [x] Reward distribution mechanism
- [x] Administrative functions

### Phase 2: Enhanced Features 🚧

- [ ] Advanced content categorization
- [ ] Time-based content ranking
- [ ] Multi-token reward support
- [ ] Content expiration mechanisms

### Phase 3: Ecosystem Growth 📋

- [ ] Frontend application development
- [ ] API integration and tooling
- [ ] Mobile application support
- [ ] Third-party integrations

## Contributing

We welcome contributions to ContentVault! Please read our contributing guidelines:

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/amazing-feature`
3. Make your changes and add tests
4. Ensure all tests pass: `npm test`
5. Commit your changes: `git commit -m 'Add amazing feature'`
6. Push to the branch: `git push origin feature/amazing-feature`
7. Open a Pull Request

### Development Guidelines

- Follow Clarity best practices and conventions
- Maintain comprehensive test coverage
- Document all public functions and significant logic
- Use meaningful commit messages
- Ensure backward compatibility when possible

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- Built on [Stacks](https://stacks.co) blockchain
- Developed with [Clarinet](https://github.com/hirosystems/clarinet)
- Inspired by decentralized content curation principles
- Community-driven development and governance

---

**ContentVault** - Transforming content discovery through collective intelligence and blockchain transparency.
