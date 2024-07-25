# Lumina Wallet Architecture

## Passkey Wallet Architecture

```mermaid
flowchart LR
    User --> |Opens Lumina Telegram Wallet| App[Telegram Wallet App]
    App --> |Selects 'Login with Passkey'| PasskeyLogin[Passkey Login]
    PasskeyLogin --> |Options: Register or Sign| RegisterOrSign[Register or Sign]
    RegisterOrSign --> |Selects 'Register'| Register[Register]
    RegisterOrSign --> |Selects 'Sign'| Sign[Sign In]
    
    Register --> |Enter Name| EnterName[Enter Name]
    EnterName --> |Create Wallet Using Stellar SDK| StellarSDK[Stellar SDK]
    StellarSDK --> Wallet[Wallet]
    Wallet --> |Save Public Key| PasskeyService[Passkey Service]
    
    Sign --> |Use Passkey| Authentication[Authentication]
    Authentication --> |Access Wallet| WalletAccess[Wallet Access]
    
    Wallet --> |Send/Receive Money| Transactions

    subgraph User Flow
        User --> App
        App --> PasskeyLogin
        PasskeyLogin --> RegisterOrSign
        RegisterOrSign --> Register
        RegisterOrSign --> Sign
        Register --> EnterName
        EnterName --> StellarSDK
        StellarSDK --> Wallet
        Wallet --> PasskeyService
        Sign --> Authentication
        Authentication --> WalletAccess
        WalletAccess --> Wallet
        Wallet --> Transactions
    end
