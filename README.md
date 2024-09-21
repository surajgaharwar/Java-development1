# Java-development1 import java.util.ArrayList;
import java.util.Scanner;

// ATM Class
class ATM {
    private double balance;
    private ArrayList<String> transactionHistory;

    public ATM() {
        this.balance = 0;
        this.transactionHistory = new ArrayList<>();
    }

    // Method to check balance
    public double checkBalance() {
        return balance;
    }

    // Method to deposit money
    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            transactionHistory.add("Deposited: $" + amount);
            System.out.println("Successfully deposited $" + amount);
        } else {
            System.out.println("Invalid deposit amount.");
        }
    }

    // Method to withdraw money
    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            transactionHistory.add("Withdrew: $" + amount);
            System.out.println("Successfully withdrew $" + amount);
        } else {
            System.out.println("Insufficient balance or invalid amount.");
        }
    }

    // Method to view transaction history
    public void viewTransactionHistory() {
        if (transactionHistory.isEmpty()) {
            System.out.println("No transactions to show.");
        } else {
            System.out.println("Transaction History:");
            for (String transaction : transactionHistory) {
                System.out.println(transaction);
            }
        }
    }
}

// User Class
class User {
    private String userId;
    private String pin;

    public User(String userId, String pin) {
        this.userId = userId;
        this.pin = pin;
    }

    public String getUserId() {
        return userId;
    }

    public String getPin() {
        return pin;
    }
}

// Main Class (ATM Interface)
public class ATMInterface {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Create a user for the ATM
        User user = new User("user123", "1234");
        ATM atm = new ATM();

        System.out.println("Welcome to the ATM Interface!");

        // Simple user authentication
        System.out.print("Enter your User ID: ");
        String enteredUserId = scanner.nextLine();

        System.out.print("Enter your PIN: ");
        String enteredPin = scanner.nextLine();

        if (!user.getUserId().equals(enteredUserId) || !user.getPin().equals(enteredPin)) {
            System.out.println("Invalid User ID or PIN. Access denied.");
            return;
        }

        boolean exit = false;

        // ATM Menu
        while (!exit) {
            System.out.println("\n--- ATM Menu ---");
            System.out.println("1. Check Balance");
            System.out.println("2. Deposit Money");
            System.out.println("3. Withdraw Money");
            System.out.println("4. View Transaction History");
            System.out.println("5. Exit");
            System.out.print("Choose an option: ");
            int choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    System.out.println("Current Balance: $" + atm.checkBalance());
                    break;
                case 2:
                    System.out.print("Enter amount to deposit: $");
                    double depositAmount = scanner.nextDouble();
                    atm.deposit(depositAmount);
                    break;
                case 3:
                    System.out.print("Enter amount to withdraw: $");
                    double withdrawAmount = scanner.nextDouble();
                    atm.withdraw(withdrawAmount);
                    break;
                case 4:
                    atm.viewTransactionHistory();
                    break;
                case 5:
                    exit = true;
                    System.out.println("Thank you for using the ATM. Goodbye!");
                    break;
                default:
                    System.out.println("Invalid choice. Please try again.");
            }
        }

        scanner.close();
    }
}
\
