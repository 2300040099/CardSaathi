# Requirements Document: CardSaathi

## Introduction

CardSaathi is an AI-powered assistant that helps Indian consumers maximize their credit and debit card rewards by recommending the optimal card for each transaction. The system analyzes transaction categories, user spending patterns, and card-specific reward policies to provide real-time recommendations that optimize cashback, rewards points, and other benefits.

## Glossary

- **CardSaathi**: The AI-powered card recommendation system
- **User**: An Indian consumer who owns multiple credit/debit cards
- **Card**: A credit card or debit card with associated reward policies
- **Transaction**: A purchase or payment made by the User
- **Transaction_Category**: The classification of a transaction (e.g., groceries, fuel, dining, travel, online shopping, utilities, entertainment)
- **Reward_Policy**: The rules defining cashback rates, reward points, and benefits for a specific Card
- **Recommendation_Engine**: The component that analyzes data and suggests optimal cards
- **Spending_Pattern**: Historical transaction data showing User behavior over time
- **Cashback_Rate**: The percentage or fixed amount returned to the User for a transaction
- **Reward_Points**: Points earned on transactions that can be redeemed for benefits
- **Benefit_Score**: A calculated value representing the total value of rewards for a card-transaction combination

## Requirements

### Requirement 1: Card Management

**User Story:** As a user, I want to add and manage my credit and debit cards in the system, so that CardSaathi can recommend from my available cards.

#### Acceptance Criteria

1. WHEN a User adds a new Card, THE CardSaathi SHALL store the card details including card type, issuer, and last four digits
2. WHEN a User adds a Card, THE CardSaathi SHALL associate the Card with the User's account
3. WHEN a User requests to view their cards, THE CardSaathi SHALL display all stored Cards with masked card numbers
4. WHEN a User removes a Card, THE CardSaathi SHALL delete the Card from the system and exclude it from future recommendations
5. THE CardSaathi SHALL support storage of at least 20 Cards per User

### Requirement 2: Reward Policy Configuration

**User Story:** As a user, I want the system to know my cards' reward policies, so that recommendations are based on accurate benefit calculations.

#### Acceptance Criteria

1. WHEN a Card is added, THE CardSaathi SHALL retrieve or allow input of the Reward_Policy for that Card
2. THE CardSaathi SHALL store Cashback_Rate and Reward_Points multipliers for each Transaction_Category per Card
3. WHEN a Reward_Policy is updated, THE CardSaathi SHALL apply the new policy to all future recommendations
4. THE CardSaathi SHALL support category-specific reward rates (e.g., 5% on groceries, 2% on fuel)
5. THE CardSaathi SHALL store additional benefits such as milestone rewards, annual fee waivers, and spending caps

### Requirement 3: Transaction Category Recognition

**User Story:** As a user, I want the system to identify transaction categories automatically or allow me to specify them, so that recommendations are accurate.

#### Acceptance Criteria

1. WHEN a User provides transaction details, THE CardSaathi SHALL classify the transaction into a Transaction_Category
2. THE CardSaathi SHALL support at least the following categories: groceries, fuel, dining, travel, online shopping, utilities, entertainment, healthcare, and general purchases
3. WHEN automatic classification is uncertain, THE CardSaathi SHALL prompt the User to confirm or select the Transaction_Category
4. WHEN a User manually specifies a Transaction_Category, THE CardSaathi SHALL use that category for the recommendation
5. THE CardSaathi SHALL learn from User corrections to improve future automatic classifications

### Requirement 4: Real-Time Card Recommendation

**User Story:** As a user, I want to receive instant card recommendations before making a transaction, so that I can use the optimal card and maximize my rewards.

#### Acceptance Criteria

1. WHEN a User requests a recommendation with transaction amount and category, THE Recommendation_Engine SHALL calculate the Benefit_Score for each Card
2. THE Recommendation_Engine SHALL recommend the Card with the highest Benefit_Score
3. WHEN multiple Cards have equal Benefit_Score, THE Recommendation_Engine SHALL recommend the Card with the lowest annual fee
4. THE CardSaathi SHALL display the recommendation within 2 seconds of receiving the request
5. THE CardSaathi SHALL show the expected cashback, reward points, and total benefit value for the recommended Card
6. THE CardSaathi SHALL display alternative card options ranked by Benefit_Score

### Requirement 5: Spending Pattern Analysis

**User Story:** As a user, I want the system to analyze my spending patterns, so that recommendations consider my historical behavior and optimize long-term rewards.

#### Acceptance Criteria

1. WHEN a User completes a transaction, THE CardSaathi SHALL record the transaction amount, category, card used, and timestamp
2. THE CardSaathi SHALL calculate monthly spending totals per Transaction_Category
3. THE CardSaathi SHALL identify spending trends over a rolling 6-month period
4. WHEN recommending a Card, THE Recommendation_Engine SHALL consider milestone rewards and spending caps based on the User's Spending_Pattern
5. WHEN a User is approaching a spending cap on a Card, THE CardSaathi SHALL factor this into the Benefit_Score calculation

### Requirement 6: Benefit Optimization

**User Story:** As a user, I want the system to maximize my total rewards across all my cards, so that I get the best value from my spending.

#### Acceptance Criteria

1. THE Recommendation_Engine SHALL calculate Benefit_Score by combining cashback value, reward points value, and additional benefits
2. WHEN calculating Benefit_Score, THE Recommendation_Engine SHALL convert reward points to monetary value using card-specific redemption rates
3. WHEN a Card has spending-based milestone rewards, THE Recommendation_Engine SHALL include progress toward milestones in the Benefit_Score
4. WHEN a Card has an annual fee, THE Recommendation_Engine SHALL amortize the fee across expected annual spending when calculating net benefit
5. THE CardSaathi SHALL provide a monthly summary showing total rewards earned and optimization opportunities

### Requirement 7: User Preferences and Constraints

**User Story:** As a user, I want to set preferences and constraints for card recommendations, so that suggestions align with my personal priorities.

#### Acceptance Criteria

1. WHEN a User sets a preference to prioritize cashback over reward points, THE Recommendation_Engine SHALL weight cashback more heavily in Benefit_Score calculations
2. WHEN a User marks a Card as unavailable, THE CardSaathi SHALL exclude that Card from recommendations until marked available again
3. WHEN a User sets a minimum benefit threshold, THE CardSaathi SHALL only recommend cards that meet or exceed that threshold
4. THE CardSaathi SHALL allow Users to set card-specific usage limits or restrictions
5. WHEN a User prefers a specific Card for a category, THE CardSaathi SHALL recommend that Card unless another Card offers significantly higher benefits (configurable threshold)

### Requirement 8: Notification and Alerts

**User Story:** As a user, I want to receive notifications about reward opportunities and important updates, so that I don't miss out on benefits.

#### Acceptance Criteria

1. WHEN a User is close to achieving a milestone reward (within 10% of spending target), THE CardSaathi SHALL notify the User
2. WHEN a Reward_Policy changes for a User's Card, THE CardSaathi SHALL alert the User within 24 hours
3. WHEN a Card's spending cap is reached, THE CardSaathi SHALL notify the User immediately
4. WHEN a better card option becomes available due to new rewards or promotions, THE CardSaathi SHALL suggest the User consider it
5. THE CardSaathi SHALL allow Users to configure notification preferences and frequency

### Requirement 9: Data Privacy and Security

**User Story:** As a user, I want my card and transaction data to be secure and private, so that I can trust the system with my financial information.

#### Acceptance Criteria

1. THE CardSaathi SHALL encrypt all Card details at rest using AES-256 encryption
2. THE CardSaathi SHALL encrypt all data in transit using TLS 1.3 or higher
3. THE CardSaathi SHALL store only the last four digits of card numbers for display purposes
4. WHEN a User deletes their account, THE CardSaathi SHALL permanently delete all associated data within 30 days
5. THE CardSaathi SHALL not share User data with third parties without explicit User consent
6. THE CardSaathi SHALL implement authentication and authorization for all User data access

### Requirement 10: Recommendation Explanation

**User Story:** As a user, I want to understand why a specific card was recommended, so that I can make informed decisions and trust the system.

#### Acceptance Criteria

1. WHEN displaying a recommendation, THE CardSaathi SHALL show the breakdown of benefits (cashback amount, reward points, additional perks)
2. THE CardSaathi SHALL display the Benefit_Score calculation methodology
3. WHEN showing alternative cards, THE CardSaathi SHALL explain why each card ranks lower than the recommended option
4. THE CardSaathi SHALL show how the recommendation considers the User's Spending_Pattern and progress toward milestones
5. THE CardSaathi SHALL provide educational content about maximizing card benefits

### Requirement 11: Multi-Card Strategy Suggestions

**User Story:** As a user, I want strategic advice on using multiple cards together, so that I can optimize my overall reward portfolio.

#### Acceptance Criteria

1. THE CardSaathi SHALL analyze the User's card portfolio and identify coverage gaps in reward categories
2. WHEN a User has suboptimal card coverage, THE CardSaathi SHALL suggest cards that would improve their portfolio
3. THE CardSaathi SHALL provide monthly insights on which cards are underutilized or overutilized
4. THE CardSaathi SHALL calculate the total annual value of the User's card portfolio based on their Spending_Pattern
5. WHEN a Card's annual fee exceeds the benefits earned, THE CardSaathi SHALL alert the User and suggest alternatives

### Requirement 12: Indian Market Specifics

**User Story:** As an Indian user, I want the system to understand India-specific payment scenarios and card features, so that recommendations are relevant to my context.

#### Acceptance Criteria

1. THE CardSaathi SHALL support Indian Rupee (INR) as the primary currency
2. THE CardSaathi SHALL recognize India-specific transaction categories such as UPI payments, wallet reloads, and bill payments
3. THE CardSaathi SHALL support Indian card issuers including HDFC, ICICI, SBI, Axis, Kotak, and others
4. THE CardSaathi SHALL account for GST implications on reward redemptions where applicable
5. THE CardSaathi SHALL support integration with popular Indian payment platforms and merchant categories
