Comprehensive Note on Class Usage in Object-Oriented Programming with a Banking System Example
Introduction to Classes in OOP
Classes are fundamental building blocks in Object-Oriented Programming (OOP) that serve as blueprints for creating objects. They encapsulate data (attributes) and behavior (methods) into a single logical unit.

Key Characteristics of Classes:
Encapsulation: Bundling data and methods that operate on that data

Abstraction: Hiding complex implementation details

Inheritance: Creating new classes from existing ones

Polymorphism: Ability to present the same interface for different underlying forms

Banking System Class Example
1. Basic Account Class
javascript
class BankAccount {
    // Constructor (special method for initializing objects)
    constructor(accountNumber, accountHolder, balance = 0) {
        // Properties (attributes)
        this._accountNumber = accountNumber;
        this._accountHolder = accountHolder;
        this._balance = balance;
        this._transactions = [];
    }

    // Methods (behaviors)
    deposit(amount) {
        if (amount <= 0) {
            throw new Error("Deposit amount must be positive");
        }
        this._balance += amount;
        this._transactions.push({
            type: 'deposit',
            amount: amount,
            date: new Date(),
            balance: this._balance
        });
        return this._balance;
    }

    withdraw(amount) {
        if (amount <= 0) {
            throw new Error("Withdrawal amount must be positive");
        }
        if (amount > this._balance) {
            throw new Error("Insufficient funds");
        }
        this._balance -= amount;
        this._transactions.push({
            type: 'withdrawal',
            amount: amount,
            date: new Date(),
            balance: this._balance
        });
        return this._balance;
    }

    getBalance() {
        return this._balance;
    }

    getAccountDetails() {
        return {
            accountNumber: this._accountNumber,
            accountHolder: this._accountHolder,
            balance: this._balance,
            transactions: this._transactions
        };
    }
}
2. Inheritance: Savings Account Class
javascript
class SavingsAccount extends BankAccount {
    constructor(accountNumber, accountHolder, balance = 0, interestRate = 0.01) {
        super(accountNumber, accountHolder, balance);
        this._interestRate = interestRate;
        this._minimumBalance = 100; // Minimum balance requirement
    }

    // Method overriding
    withdraw(amount) {
        if (this._balance - amount < this._minimumBalance) {
            throw new Error(`Cannot withdraw. Minimum balance of ${this._minimumBalance} must be maintained`);
        }
        super.withdraw(amount);
    }

    applyInterest() {
        const interest = this._balance * this._interestRate;
        this.deposit(interest);
        return interest;
    }

    getInterestRate() {
        return this._interestRate;
    }
}
3. Inheritance: Current Account Class
javascript
class CurrentAccount extends BankAccount {
    constructor(accountNumber, accountHolder, balance = 0, overdraftLimit = 500) {
        super(accountNumber, accountHolder, balance);
        this._overdraftLimit = overdraftLimit;
    }

    // Method overriding
    withdraw(amount) {
        if (amount <= 0) {
            throw new Error("Withdrawal amount must be positive");
        }
        if (amount > (this._balance + this._overdraftLimit)) {
            throw new Error("Exceeds overdraft limit");
        }
        this._balance -= amount;
        this._transactions.push({
            type: 'withdrawal',
            amount: amount,
            date: new Date(),
            balance: this._balance
        });
        return this._balance;
    }

    getOverdraftLimit() {
        return this._overdraftLimit;
    }
}
4. Composition: Bank Class (Managing Multiple Accounts)
javascript
class Bank {
    constructor(name) {
        this._name = name;
        this._accounts = [];
    }

    openAccount(account) {
        if (!(account instanceof BankAccount)) {
            throw new Error("Can only add BankAccount objects");
        }
        this._accounts.push(account);
        return account.getAccountDetails();
    }

    closeAccount(accountNumber) {
        const index = this._accounts.findIndex(acc => acc._accountNumber === accountNumber);
        if (index === -1) {
            throw new Error("Account not found");
        }
        const account = this._accounts[index];
        if (account.getBalance() !== 0) {
            throw new Error("Account balance must be zero before closing");
        }
        this._accounts.splice(index, 1);
        return `Account ${accountNumber} closed successfully`;
    }

    getTotalDeposits() {
        return this._accounts.reduce((total, account) => total + account.getBalance(), 0);
    }

    applyAnnualInterest() {
        this._accounts.forEach(account => {
            if (account instanceof SavingsAccount) {
                account.applyInterest();
            }
        });
    }

    findAccount(accountNumber) {
        const account = this._accounts.find(acc => acc._accountNumber === accountNumber);
        if (!account) {
            throw new Error("Account not found");
        }
        return account;
    }
}
Key OOP Concepts Demonstrated in Banking Example
1. Encapsulation
All account details are protected (using _ convention for private properties)

Access to balance is controlled through methods

2. Inheritance
SavingsAccount and CurrentAccount inherit from BankAccount

Inherited methods can be overridden (e.g., different withdrawal rules)

3. Polymorphism
Different account types can be treated uniformly as BankAccount objects

The Bank class can manage any type of account that inherits from BankAccount

4. Abstraction
Complex operations like interest calculation are hidden in methods

Users interact with simple interfaces (deposit, withdraw) without knowing internal details

Best Practices for Class Design in Banking Systems
Single Responsibility Principle: Each class should have one responsibility

BankAccount manages basic transactions

SavingsAccount handles interest-specific logic

Bank manages account collection

Loose Coupling: Classes should depend on abstractions rather than concrete implementations

Immutable Properties: Critical properties like account numbers shouldn't be changeable after creation

Error Handling: Validate inputs and throw appropriate exceptions

Documentation: Clearly document each class's purpose and usage

Advanced Class Features in Banking Context
1. Static Methods and Properties
javascript
class BankAccount {
    static accountCounter = 1000;
    static generateAccountNumber() {
        return `ACCT-${BankAccount.accountCounter++}`;
    }
    
    constructor(accountHolder, balance) {
        this._accountNumber = BankAccount.generateAccountNumber();
        // ... rest of constructor
    }
}
2. Private Class Fields (Modern JavaScript)
javascript
class BankAccount {
    #accountNumber; // Truly private field
    #balance;
    
    constructor(accountNumber, accountHolder, balance = 0) {
        this.#accountNumber = accountNumber;
        this.#balance = balance;
        // ... rest of constructor
    }
    
    // Public method to access private field
    getAccountNumber() {
        return this.#accountNumber;
    }
}
3. Interfaces/Abstract Classes (Conceptual in JavaScript)
javascript
// Conceptual example - JavaScript doesn't have real abstract classes
class Account {
    constructor() {
        if (new.target === Account) {
            throw new Error("Cannot instantiate abstract class");
        }
    }
    
    deposit() {
        throw new Error("Method 'deposit()' must be implemented");
    }
    
    withdraw() {
        throw new Error("Method 'withdraw()' must be implemented");
    }
}
Real-world Banking System Considerations
Transaction Processing: More sophisticated transaction handling with rollback capabilities

Security: Encryption of sensitive data, authentication

Audit Logging: Comprehensive tracking of all operations

Concurrency Control: Handling simultaneous transactions

Persistence: Database integration for long-term storage

This comprehensive example demonstrates how classes can effectively model complex real-world systems like banking, providing structure, maintainability, and extensibility to the codebase.


*Author*
Onaolapo Abiodun