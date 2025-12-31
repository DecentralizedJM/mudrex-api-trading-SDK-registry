# Mudrex SDK Registry

Comprehensive registry of all Mudrex Futures Trading API SDKs. Each SDK provides a type-safe, production-ready interface for building trading strategies.

**All SDKs are Unofficial** and built & maintained by [DecentralizedJM](https://github.com/DecentralizedJM). For the official API documentation, visit [Mudrex Trading API Docs](https://docs.trade.mudrex.com/docs/overview).

## ✅ Status: Production Ready

All SDKs have been thoroughly tested and audited. Latest updates:
- ✅ HTTP method bugs fixed (wallet endpoints)
- ✅ Model field mapping corrected to match actual API responses
- ✅ Error handling improved for edge cases
- ✅ Added missing status values (e.g., LIQUIDATED position status)
- ✅ Backwards compatibility maintained where possible

---

## 📚 Available SDKs

### 🐍 Python SDK
**Repository:** https://github.com/DecentralizedJM/mudrex-trading-sdk

A comprehensive Python SDK for Mudrex Futures Trading API with full async/await support.

#### Features
- Fully async with asyncio
- Type hints and mypy compatible
- Built-in rate limiting
- Comprehensive error handling
- Zero external dependencies

#### Installation
```bash
pip install mudrex-trading-sdk
```

#### Quick Example
```python
import asyncio
from mudrex_trading_sdk import MudrexClient

async def main():
    client = MudrexClient("your-api-key")
    balance = await client.wallet.get_spot_balance()
    print(f"Balance: {balance.total}")

asyncio.run(main())
```

---

### 🐹 Go SDK
**Repository:** https://github.com/DecentralizedJM/mudrex-go-sdk

A high-performance Go SDK for Mudrex Futures Trading API with concurrent request support.

#### Features
- Goroutine-friendly async design
- Strongly typed with interfaces
- Built-in rate limiting with channels
- Comprehensive error wrapping
- Zero external dependencies (standard library only)

#### Installation
```bash
go get github.com/DecentralizedJM/mudrex-go-sdk
```

#### Quick Example
```go
package main

import (
	"fmt"
	"github.com/DecentralizedJM/mudrex-go-sdk"
)

func main() {
	client := mudrex.NewClient("your-api-key")
	balance, err := client.Wallet.GetSpotBalance(context.Background())
	if err != nil {
		panic(err)
	}
	fmt.Printf("Balance: %s\n", balance.Total)
}
```

---

### ☕ Java SDK
**Repository:** https://github.com/DecentralizedJM/mudrex-java-sdk

An enterprise-ready Java SDK for Mudrex Futures Trading API with Maven support.

#### Features
- Full Maven integration
- Comprehensive Javadoc
- Built-in rate limiting with concurrent utilities
- Robust error handling and validation
- Minimal dependencies (only Gson)

#### Installation (Maven)
```xml
<dependency>
    <groupId>com.mudrex</groupId>
    <artifactId>mudrex-sdk</artifactId>
    <version>1.0.0</version>
</dependency>
```

#### Quick Example
```java
public class MudrexExample {
    public static void main(String[] args) throws Exception {
        MudrexClient client = new MudrexClient("your-api-key");
        WalletBalance balance = client.wallet.getSpotBalance();
        System.out.println("Balance: " + balance.getTotal());
    }
}
```

---

### 🔷 .NET SDK
**Repository:** https://github.com/DecentralizedJM/mudrex-dotnet-sdk

A modern C# .NET SDK for Mudrex Futures Trading API with NuGet packaging.

#### Features
- Full async/await support
- Nullable reference types enabled
- Integrated with NuGet ecosystem
- Built-in rate limiting with SemaphoreSlim
- Zero external dependencies (.NET built-in only)

#### Installation (NuGet)
```bash
dotnet add package Mudrex.TradingSDK
```

Or via Package Manager:
```powershell
Install-Package Mudrex.TradingSDK
```

#### Quick Example
```csharp
using Mudrex.TradingSDK;

var client = new MudrexClient("your-api-key");
var balance = await client.Wallet.GetSpotBalanceAsync();
Console.WriteLine($"Balance: {balance.Total}");
```

---

### 📘 Node.js SDK
**Repository:** https://github.com/DecentralizedJM/mudrex-nodejs-sdk

A TypeScript-first Node.js SDK for Mudrex Futures Trading API with full type safety.

#### Features
- Full TypeScript support
- Promise-based async design
- Built-in rate limiting with timers
- Comprehensive error hierarchy
- Minimal dependencies (only Axios)

#### Installation (npm)
```bash
npm install mudrex-trading-sdk
```

#### Quick Example
```typescript
import { MudrexClient } from 'mudrex-trading-sdk';

const client = new MudrexClient('your-api-key');
const balance = await client.wallet.getSpotBalance();
console.log(`Balance: ${balance.total}`);
```

---

## 🔄 API Modules

All SDKs implement the following 6 API modules with consistent interfaces:

### 1. Wallet API
Manage spot and futures balances, transfer assets between wallets.

```
GET  /wallet/balance?type=SPOT        → Get spot balance
GET  /wallet/balance?type=FUTURES     → Get futures balance
POST /wallet/transfer                 → Transfer between wallets
```

### 2. Assets API
List and retrieve asset details, trading pairs, fees.

```
GET /assets              → List all assets
GET /assets/{assetId}    → Get specific asset details
```

### 3. Leverage API
Manage trading leverage for futures positions.

```
GET  /futures/{assetId}/leverage      → Get current leverage
POST /futures/{assetId}/leverage      → Set leverage
```

### 4. Orders API
Create, manage, and track orders across all assets.

```
POST   /futures/{assetId}/order       → Create order
GET    /orders                         → List open orders
GET    /orders/{orderId}               → Get order details
GET    /orders/history                 → Get order history
PATCH  /orders/{orderId}               → Amend order
DELETE /orders/{orderId}               → Cancel order
```

### 5. Positions API
Manage open positions, set risk orders (SL/TP), close/reverse positions.

```
GET    /positions                      → List open positions
GET    /positions/{positionId}         → Get position details
POST   /positions/{positionId}/close   → Close position
POST   /positions/{positionId}/reverse → Reverse position
POST   /positions/{positionId}/risk-order       → Set risk order
PATCH  /positions/{positionId}/risk-order/{id}  → Edit risk order
GET    /positions/history              → Get position history
```

### 6. Fees API
Retrieve fee history and trading fee details.

```
GET /fees/history   → Get fee history with pagination
```

---

## 🛡️ Error Handling

All SDKs provide a consistent error hierarchy:

| Exception | HTTP Status | Description |
|-----------|-------------|-------------|
| `MudrexAuthenticationException` | 401 | Invalid or missing API key |
| `MudrexRateLimitException` | 429 | Rate limit exceeded (>2 req/sec) |
| `MudrexValidationException` | 400 | Invalid request parameters |
| `MudrexNotFoundException` | 404 | Resource not found |
| `MudrexConflictException` | 409 | Conflicting operation |
| `MudrexInsufficientBalanceException` | 400 | Not enough balance |
| `MudrexServerException` | 500+ | Server-side error |
| `MudrexException` | Generic | Base exception class |

### Python Example
```python
from mudrex_trading_sdk import (
    MudrexRateLimitException,
    MudrexInsufficientBalanceException
)

try:
    await client.orders.create_limit_order(...)
except MudrexInsufficientBalanceException as e:
    print(f"Insufficient balance: {e}")
except MudrexRateLimitException as e:
    print(f"Rate limited, retry later")
```

---

## ⚙️ Configuration

All SDKs support custom configuration:

### API Key
Required for all requests. Set via constructor or environment variable.

### Base URL
Default: `https://trade.mudrex.com/fapi/v1`

Can be customized for testing or using different instances.

### Rate Limiting
Default: 2 requests/second (enforced by Mudrex API)

Can be customized per SDK, but respects server-side limits.

---

## 📊 Comparison Matrix

| Feature | Python | Go | Java | .NET | Node.js |
|---------|--------|----|----|------|---------|
| **Async Support** | ✅ asyncio | ✅ goroutines | ✅ CompletableFuture | ✅ async/await | ✅ Promise |
| **Type Safety** | ✅ Type Hints | ✅ Interfaces | ✅ Generics | ✅ Nullable Types | ✅ TypeScript |
| **Rate Limiting** | ✅ Built-in | ✅ Built-in | ✅ Built-in | ✅ Built-in | ✅ Built-in |
| **Error Handling** | ✅ 8 Types | ✅ 8 Types | ✅ 8 Types | ✅ 8 Types | ✅ 8 Types |
| **External Dependencies** | None | None | Gson | None | Axios |
| **Package Manager** | pip | go get | Maven | NuGet | npm |
| **Documentation** | ✅ Full | ✅ Full | ✅ Javadoc | ✅ XML Docs | ✅ TSDoc |
| **Examples** | ✅ Yes | ✅ Yes | ✅ Yes | ✅ Yes | ✅ Yes |
| **Community** | Active | Active | Active | Active | Active |

---

## 🚀 Getting Started

### 1. Choose Your SDK
Select the SDK for your preferred language.

### 2. Get API Key
Visit [Mudrex](https://mudrex.com) and generate an API key with trading permissions.

### 3. Install the SDK
Use your language's package manager (pip, go get, Maven, NuGet, npm).

### 4. Initialize Client
```
client = new MudrexClient("your-api-key")
```

### 5. Start Trading
Use any of the 6 API modules to build your strategy.

---

## 📖 Examples

### Trading Strategy Example (Python)

```python
import asyncio
from mudrex_trading_sdk import MudrexClient, OrderSide

async def simple_dca_strategy():
    client = MudrexClient("your-api-key")
    
    # Check balance
    balance = await client.wallet.get_futures_balance()
    available = float(balance.available)
    
    # Dollar-cost average
    order_size = available / 10  # Trade 10% of balance
    
    # Place limit order
    order = await client.orders.create_limit_order(
        asset_id="BTCUSD",
        side=OrderSide.BUY,
        quantity=str(order_size),
        price="50000"
    )
    print(f"Order placed: {order.id}")
    
    # Set risk orders
    position = (await client.positions.list_open())[0]
    await client.positions.set_stop_loss(position.id, "48000")
    await client.positions.set_take_profit(position.id, "52000")

asyncio.run(simple_dca_strategy())
```

### Grid Trading Example (Node.js)

```typescript
import { MudrexClient, OrderSide, OrderType } from 'mudrex-trading-sdk';

async function gridTradingStrategy() {
  const client = new MudrexClient('your-api-key');
  
  const gridLevels = [49000, 49500, 50000, 50500, 51000];
  
  for (const price of gridLevels) {
    const order = await client.orders.create({
      side: OrderSide.BUY,
      type: OrderType.LIMIT,
      quantity: '0.01',
      price: price.toString(),
    });
    console.log(`Grid order at ${price}: ${order.id}`);
  }
}

gridTradingStrategy();
```

---

## 🤝 Contributing

All SDKs welcome contributions! 

- Report bugs via GitHub Issues
- Submit features via Pull Requests
- Share examples and improvements
- Help with documentation

---

## 📄 License

All SDKs are released under the MIT License. See individual repositories for details.

---

## ⚠️ Disclaimer

These are **UNOFFICIAL** SDKs maintained by the community. They are provided as-is for educational and development purposes. Users are responsible for:

- Securing their API keys
- Validating all trading logic before deployment
- Understanding the risks of automated trading
- Complying with local regulations

Use at your own risk. Always test thoroughly in a safe environment before using with real capital.

---

## 📞 Support

For SDK-specific issues, open an issue on the respective GitHub repository:
- [Python SDK Issues](https://github.com/DecentralizedJM/mudrex-trading-sdk/issues)
- [Go SDK Issues](https://github.com/DecentralizedJM/mudrex-go-sdk/issues)
- [Java SDK Issues](https://github.com/DecentralizedJM/mudrex-java-sdk/issues)
- [.NET SDK Issues](https://github.com/DecentralizedJM/mudrex-dotnet-sdk/issues)
- [Node.js SDK Issues](https://github.com/DecentralizedJM/mudrex-nodejs-sdk/issues)

For Mudrex API questions, check the [official documentation](https://docs.trade.mudrex.com/docs/overview).

---

**Last Updated:** December 31, 2024
**Built and maintained by [DecentralizedJM](https://github.com/DecentralizedJM)**
