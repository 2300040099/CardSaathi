# CardSaathi 💳

**AI-Powered Credit Card Recommendation System for Indian Consumers**

CardSaathi helps you maximize cashback, rewards, and benefits by recommending the best credit or debit card for every transaction. Built specifically for the Indian market with support for UPI, popular Indian card issuers, and INR-based calculations.

## 🎯 What is CardSaathi?

CardSaathi analyzes your transaction category, spending behavior, and card reward policies to give real-time suggestions on which card to use. Stop leaving money on the table—let CardSaathi optimize your rewards automatically.

### Key Features

- **Smart Recommendations**: Get instant card suggestions based on transaction category and amount
- **Benefit Optimization**: Maximize cashback, reward points, and milestone progress
- **Spending Analytics**: Track your spending patterns and identify optimization opportunities
- **Multi-Card Strategy**: Analyze your card portfolio and get suggestions to improve coverage
- **Indian Market Focus**: Support for UPI, Indian issuers (HDFC, ICICI, SBI, Axis, Kotak), and INR calculations
- **Privacy-First**: Your card data is encrypted and never shared with third parties

## 🚀 Quick Start

### Prerequisites

- Node.js 18+ and npm
- PostgreSQL 14+
- Redis 6+

### Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/card-saathi.git
cd card-saathi

# Install dependencies
npm install

# Set up environment variables
cp .env.example .env
# Edit .env with your database and Redis credentials

# Run database migrations
npm run migrate

# Seed sample card reward policies
npm run seed

# Start the development server
npm run dev
```

The API will be available at `http://localhost:3000`

## 📖 Usage

### Add Your Cards

```bash
POST /api/cards
{
  "cardType": "credit",
  "issuer": "HDFC",
  "lastFourDigits": "1234",
  "cardNetwork": "Visa",
  "expiryMonth": 12,
  "expiryYear": 2025,
  "annualFee": 1000,
  "rewardPolicyId": "hdfc-regalia-policy-id"
}
```

### Get Card Recommendation

```bash
POST /api/recommendations
{
  "amount": 5000,
  "category": "groceries"
}
```

**Response:**
```json
{
  "recommendedCard": {
    "id": "card-123",
    "issuer": "HDFC",
    "lastFourDigits": "1234"
  },
  "benefitScore": {
    "totalScore": 250,
    "cashbackValue": 200,
    "rewardPointsValue": 50
  },
  "estimatedBenefit": {
    "cashback": 200,
    "rewardPoints": 100,
    "rewardPointsValueInINR": 50,
    "totalBenefitINR": 250,
    "effectiveDiscountPercent": 5.0
  },
  "explanation": {
    "primaryReason": "Highest cashback rate for groceries category",
    "benefitBreakdown": [
      "4% cashback on groceries = ₹200",
      "2x reward points = 100 points worth ₹50"
    ]
  }
}
```

### Record a Transaction

```bash
POST /api/transactions
{
  "cardId": "card-123",
  "amount": 5000,
  "category": "groceries",
  "merchantName": "BigBasket"
}
```

### View Monthly Summary

```bash
GET /api/analytics/monthly-summary?month=2024-01
```

## 🏗️ Architecture

CardSaathi follows a modular, layered architecture:

```
┌─────────────────────────────────────┐
│      User Interface Layer           │
│   (Web App / Mobile App / API)      │
└─────────────────────────────────────┘
                 │
┌─────────────────────────────────────┐
│         API Gateway                  │
│  (Authentication, Rate Limiting)     │
└─────────────────────────────────────┘
                 │
┌─────────────────────────────────────┐
│        Core Services                 │
│  • Card Management                   │
│  • Reward Policy Engine              │
│  • Recommendation Engine             │
│  • Spending Analytics                │
│  • Notification Service              │
└─────────────────────────────────────┘
                 │
┌─────────────────────────────────────┐
│         Data Layer                   │
│  PostgreSQL + Redis Cache            │
└─────────────────────────────────────┘
```

### Core Components

- **Card Management Service**: CRUD operations for user cards
- **Reward Policy Engine**: Stores and retrieves card-specific reward policies
- **Recommendation Engine**: Calculates benefit scores and generates recommendations
- **Spending Analytics Service**: Analyzes transaction history and identifies patterns
- **Notification Service**: Sends alerts for milestones, policy changes, and opportunities

## 🧪 Testing

CardSaathi uses a dual testing approach:

- **Unit Tests**: Specific examples, edge cases, and error conditions
- **Property-Based Tests**: Universal properties verified across random inputs (100+ iterations)

```bash
# Run all tests
npm test

# Run unit tests only
npm run test:unit

# Run property-based tests
npm run test:property

# Run with coverage
npm run test:coverage
```

### Test Coverage

- 33 correctness properties validated through property-based testing
- Minimum 80% line coverage, 75% branch coverage
- All critical paths (recommendation engine, benefit calculation) have 95%+ coverage

## 📊 Supported Card Issuers

CardSaathi includes pre-configured reward policies for major Indian card issuers:

- HDFC Bank (Regalia, Diners Club, Millennia)
- ICICI Bank (Amazon Pay, Coral, Sapphiro)
- SBI Cards (SimplyCLICK, Prime, Elite)
- Axis Bank (Magnus, Ace, Flipkart)
- Kotak Mahindra (811, Zen, Royale)

You can also add custom reward policies for any card.

## 🔒 Security & Privacy

- **Encryption at Rest**: All card details encrypted with AES-256
- **Encryption in Transit**: TLS 1.3 for all API communications
- **Data Minimization**: Only last 4 digits of card numbers stored
- **Access Control**: JWT-based authentication and authorization
- **GDPR Compliance**: Account deletion removes all user data within 30 days

## 📈 Performance

- **Sub-2-second recommendations**: Optimized with Redis caching
- **Scalable architecture**: Handles 1000+ cards and 10,000+ transactions per user
- **Efficient queries**: Indexed database queries for fast retrieval

## 🛣️ Roadmap

- [ ] Mobile app (iOS and Android)
- [ ] Browser extension for automatic recommendations during online shopping
- [ ] Integration with popular Indian payment apps
- [ ] Machine learning for improved category classification
- [ ] Support for international cards and multi-currency transactions
- [ ] Shared family card portfolios

## 📝 Documentation

- [Requirements Document](.kiro/specs/card-saathi/requirements.md)
- [Design Document](.kiro/specs/card-saathi/design.md)
- [Implementation Tasks](.kiro/specs/card-saathi/tasks.md)
- [API Documentation](docs/api.md) _(coming soon)_

## 🤝 Contributing

Contributions are welcome! Please read our [Contributing Guide](CONTRIBUTING.md) for details on our code of conduct and the process for submitting pull requests.

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Built with the requirements-first workflow using EARS patterns and INCOSE quality rules
- Property-based testing inspired by QuickCheck and Hypothesis
- Designed specifically for the Indian credit card market

## 📧 Contact

For questions, suggestions, or support:
- Email: support@cardsaathi.com
- Twitter: [@CardSaathi](https://twitter.com/cardsaathi)
- GitHub Issues: [Report a bug](https://github.com/yourusername/card-saathi/issues)

---

**Made with ❤️ for Indian consumers who want to maximize their credit card rewards**
