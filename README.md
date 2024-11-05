class ATM:
    def __init__(self, account_number, pin, balance=0):
        self.account_number = account_number
        self.pin = pin
        self.balance = balance
        self.transaction_history = []

    def authenticate(self, pin):
        """Verify the PIN"""
        return self.pin == pin

    def check_balance(self):
        """Display the current balance"""
        return self.balance

    def withdraw(self, amount):
        """Withdraw cash"""
        if amount > self.balance:
            return "Insufficient funds"
        self.balance -= amount
        self.transaction_history.append(f"Withdrawal: -${amount}")
        return f"Withdrawal successful. New balance: ${self.balance}"

    def deposit(self, amount):
        """Deposit cash"""
        self.balance += amount
        self.transaction_history.append(f"Deposit: +${amount}")
        return f"Deposit successful. New balance: ${self.balance}"

    def change_pin(self, old_pin, new_pin):
        """Change the PIN"""
        if self.authenticate(old_pin):
            self.pin = new_pin
            return "PIN changed successfully"
        return "Invalid old PIN"

    def transaction_history(self):
        """Display transaction history"""
        return self.transaction_history

def main():
    # Initialize ATM with account number, PIN, and balance
    atm = ATM("123456789", 1234, 1000)

    while True:
        print("\nATM Menu:")
        print("1. Check Balance")
        print("2. Withdraw")
        print("3. Deposit")
        print("4. Change PIN")
        print("5. Transaction History")
        print("6. Exit")

        choice = input("Enter your choice: ")

        if choice == "1":
            pin = int(input("Enter PIN: "))
            if atm.authenticate(pin):
                print(f"Balance: ${atm.check_balance()}")
            else:
                print("Invalid PIN")
        elif choice == "2":
            pin = int(input("Enter PIN: "))
            if atm.authenticate(pin):
                amount = float(input("Enter withdrawal amount: "))
                print(atm.withdraw(amount))
            else:
                print("Invalid PIN")
        elif choice == "3":
            pin = int(input("Enter PIN: "))
            if atm.authenticate(pin):
                amount = float(input("Enter deposit amount: "))
                print(atm.deposit(amount))
            else:
                print("Invalid PIN")
        elif choice == "4":
            pin = int(input("Enter old PIN: "))
            new_pin = int(input("Enter new PIN: "))
            print(atm.change_pin(pin, new_pin))
        elif choice == "5":
            pin = int(input("Enter PIN: "))
            if atm.authenticate(pin):
                print("\nTransaction History:")
                for transaction in atm.transaction_history:
                    print(transaction)
            else:
                print("Invalid PIN")
        elif choice == "6":
            break
        else:
            print("Invalid choice. Please try again.")

if __name__ == "__main__":
    main()
