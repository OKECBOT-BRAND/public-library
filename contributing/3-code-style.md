# Code Style & Standards

## General Guidelines

- **Readability** over cleverness
- **Consistency** with existing code
- **Documentation** for all public APIs
- **Tests** for all new features and bug fixes

## PHP Standards

### PSR-12 Compliance

All PHP code must follow [PSR-12](https://www.php-fig.org/psr/psr-12/) standards.

### Class Structure

```php
<?php

declare(strict_types=1);

namespace Okecbot\Marketplace;

use Okecbot\Contracts\PaymentGateway;
use Okecbot\Exceptions\EscrowException;
use Psr\Log\LoggerInterface;

/**
 * Manages escrow holds for leased sessions.
 * 
 * This class processes payments, calculates commission, and generates secure tokens.
 */
final class EscrowManager
{
    private PaymentGateway $gateway;
    private LoggerInterface $logger;

    public function __construct(PaymentGateway $gateway, LoggerInterface $logger)
    {
        $this->gateway = $gateway;
        $this->logger = $logger;
    }

    /**
     * Holds funds in escrow for a transaction.
     * 
     * @throws EscrowException If amount is invalid or gateway fails
     */
    public function hold(string $transactionId, float $amount, string $type): void
    {
        if ($amount < 1000.0) {
            throw EscrowException::invalidAmount($amount);
        }
        
        $commission = $amount * 0.10;
        
        $this->logger->info('Processing escrow hold', [
            'transaction' => $transactionId,
            'amount' => $amount,
            'type' => $type
        ]);
        
        $this->gateway->hold($transactionId, $amount);
    }
}
```

### Type Declarations

- Use strict types (`declare(strict_types=1)`)
- Type hint all method parameters and return types
- Use PHP 8.0+ features where available

## JavaScript/TypeScript Standards

### ESLint + Prettier

All JavaScript/TypeScript code must pass:

```bash
npm run lint
npm run format
```

### React Components

```jsx
import React from 'react';
import PropTypes from 'prop-types';

/**
 * Displays a user profile card with avatar and basic info.
 */
const UserProfile = ({ user, onEdit }) => (
  <div className="user-profile">
    <img 
      src={user.avatar} 
      alt={`${user.name}'s avatar`} 
      className="avatar"
    />
    <h2>{user.name}</h2>
    <p>{user.bio}</p>
    <button onClick={onEdit}>
      Edit Profile
    </button>
  </div>
);

UserProfile.propTypes = {
  user: PropTypes.shape({
    name: PropTypes.string.isRequired,
    avatar: PropTypes.string.isRequired,
    bio: PropTypes.string,
  }).isRequired,
  onEdit: PropTypes.func.isRequired,
};

export default UserProfile;
```

## Database

### Naming Conventions

- Tables: `snake_case` plural (e.g., `user_profiles`)
- Columns: `snake_case`
- Primary keys: `id`
- Foreign keys: `table_name_id`
- Timestamps: `created_at`, `updated_at`, `deleted_at`

### Migrations

- One feature/change per migration
- Include both `up` and `down` methods
- Add indexes for frequently queried columns

## Documentation

### Inline Comments

- Use docblocks for all public methods and classes
- Explain "why" not just "what"
- Keep comments up to date with code changes

### README Files

Each repository must include:
- Project description
- Installation instructions
- Configuration
- Usage examples
- Development setup
- Testing instructions
- Deployment notes

## Next Steps

- [Testing Guidelines →](4-testing.md)
- [Pull Request Process →](5-pull-requests.md)
