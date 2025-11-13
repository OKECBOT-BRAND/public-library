# Testing Guidelines

## Testing Philosophy

- **Test First**: Write tests before or alongside implementation
- **Meaningful Tests**: Focus on behavior, not implementation
- **Isolation**: Tests should be independent and not rely on external services
- **Readability**: Tests should be clear and serve as documentation

## Test Structure

### Unit Tests

- Test individual functions/methods in isolation
- Mock all external dependencies
- Follow the Arrange-Act-Assert pattern

```javascript
// Example Unit Test (Jest)
describe('UserService', () => {
  let userService;
  let mockUserRepository;

  beforeEach(() => {
    mockUserRepository = {
      findById: jest.fn(),
      save: jest.fn()
    };
    userService = new UserService(mockUserRepository);
  });

  describe('getUser', () => {
    it('should return user when found', async () => {
      // Arrange
      const mockUser = { id: 1, name: 'Test User' };
      mockUserRepository.findById.mockResolvedValue(mockUser);

      // Act
      const result = await userService.getUser(1);

      // Assert
      expect(result).toEqual(mockUser);
      expect(mockUserRepository.findById).toHaveBeenCalledWith(1);
    });
  });
});
```

### Integration Tests

- Test interactions between components
- Use test databases (e.g., SQLite in-memory)
- Clean up after each test

```php
// Example Integration Test (PHPUnit)
class UserControllerTest extends TestCase
{
    private EntityManagerInterface $entityManager;
    private UserController $controller;

    protected function setUp(): void
    {
        $kernel = self::bootKernel();
        $this->entityManager = $kernel->getContainer()
            ->get('doctrine')
            ->getManager();
            
        $this->controller = new UserController(
            $this->entityManager,
            $this->createMock(LoggerInterface::class)
        );
    }

    public function testCreateUser(): void
    {
        $userData = [
            'email' => 'test@example.com',
            'password' => 'secure123',
            'name' => 'Test User'
        ];

        $response = $this->controller->create(new Request([], $userData));
        $this->assertEquals(201, $response->getStatusCode());
        
        $user = $this->entityManager
            ->getRepository(User::class)
            ->findOneBy(['email' => 'test@example.com']);
            
        $this->assertNotNull($user);
        $this->assertEquals('Test User', $user->getName());
    }
}
```

### End-to-End Tests

- Test critical user flows
- Use tools like Cypress or Playwright
- Run against a staging environment

## Test Coverage

- Aim for at least 80% code coverage
- Focus on business logic, not getters/setters
- Cover edge cases and error conditions

## Performance Testing

- Test with realistic data volumes
- Monitor memory usage and response times
- Set performance budgets

## Security Testing

- Include security tests in CI/CD
- Test for common vulnerabilities (OWASP Top 10)
- Regular dependency updates

## Running Tests

### Local Development

```bash
# Run all tests
npm test

# Run specific test file
npm test path/to/test.spec.js

# Run with coverage
npm run test:coverage
```

### CI/CD

- Run tests on every push
- Require all tests to pass before merge
- Generate coverage reports

## Test Data

- Use factories/fixtures for consistent test data
- Consider using Faker for realistic test data
- Clean up test data after tests

## Best Practices

1. **Test Naming**: `methodName_StateUnderTest_ExpectedBehavior`
2. **One Assertion Per Test**: Focus on one behavior per test
3. **Descriptive Names**: Make test names clear and descriptive
4. **Test Edge Cases**: Include boundary conditions and error cases
5. **Keep Tests Fast**: Mock expensive operations

## Next Steps

- [Pull Request Process →](5-pull-requests.md)
- [Release Process →](6-release-process.md)
