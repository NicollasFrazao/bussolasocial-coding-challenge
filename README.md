# Bússola Social Challenge - Shopping cart total calculator

A dependency-free PHP class that works out a shopping cart's final price from its items and the chosen payment method, with PHPUnit tests.

## Context

Solution to the hiring challenge of Bússola Social (2025). The challenge statement is kept in Portuguese in [`docs/challenge.md`](docs/challenge.md). Its rules:

- Each cart item has a name, a unit price and a quantity.
- Payment methods: Pix (paid at once), credit card paid at once (1x), and credit card in 2 to 12 installments.
- Paying at once gets a 10% discount.
- Installments add 1% interest per month, compounded: `M = P * (1 + i)^n`.
- No database, API or payment gateway; a unit test is encouraged.

## What it does

`app/Services/CartService.php` defines `CartService`:

```php
new CartService(array $items, string $payment_method, int $installment_quantity = 1)
```

- **Items** are arrays with `name`, `unit_price` and `quantity`. A missing key, or a negative price or quantity, throws an `Exception` with a Portuguese message.
- **Payment methods** come from `getAvailablePaymentMethods()`, which returns `pix` and `credit`. Any other value throws.
- **Installments** must be exactly `1` for `pix` and between `2` and `12` for `credit`.
- `getFinalValue()` adds up `unit_price * quantity`. With one installment it applies a 10% discount. Otherwise it multiplies by `1.01^n`.
- The class has getters and setters for items, payment method and installments.
- Card holder data (name, number, expiry, CVV) is not modelled. The class docblock explains that this data does not affect the result.

Example:

```php
require 'app/Services/CartService.php';

$items = [['name' => 'Product', 'unit_price' => 100, 'quantity' => 1]];

(new CartService($items, 'pix'))->getFinalValue();        // 90
(new CartService($items, 'credit', 2))->getFinalValue();  // 102.01
```

## Tech stack

- Plain PHP: no framework, no Composer. The class uses typed properties, so it needs PHP 7.4+.
- PHPUnit 10.5.46, bundled as `phpunit.phar` (needs PHP 8.1+). The tests use `#[Depends]` attributes.

## Running the tests

```bash
php phpunit.phar tests/CartServiceTest.php
```

Checked with PHP 8.3: `OK (17 tests, 19 assertions)`.

Without a local PHP 8.1+:

```bash
docker run --rm -v "$PWD":/app -w /app php:8.3-cli php phpunit.phar tests/CartServiceTest.php
```

## Project structure

```
app/Services/CartService.php   The calculator
tests/CartServiceTest.php      PHPUnit tests (construction, setters, validation errors)
phpunit.phar                   Bundled PHPUnit 10.5.46
```

## Notes

- "Credit card paid at once (1x)" cannot be expressed: `credit` rejects 1 installment, so the 10% discount is only reachable through `pix`.
- `setPaymentMethod()` does not re-check the installment count. After `setPaymentMethod('pix')` on a cart built as `credit` with 12 installments, the cart still applies interest.
- The error message for an invalid `credit` installment count says "pix" and "between 1 and 12".
- `getFinalValue()` does not round its float result.
- The tests check construction, the setters and the validation errors. The only test on the price, `testGetFinalValue`, asserts that the result is a float, not its amount.
- The statement asks for the main class to be used to compute the total for each of the three payment methods. The repository has no such script, only the tests.
- `phpunit.phar` (about 5 MB) and `.phpunit.result.cache` are committed.
