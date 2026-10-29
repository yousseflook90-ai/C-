#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;


class Account {
private:
    string name;
    int number;
    double balance;
public:
    int getNumber() {return number;} string getName() {return name;} double getBalance() {return balance;}
    Account(string account_name, int account_number, double account_balance) {
        name = account_name;
        number = account_number;
        balance = account_balance;
    }
    string deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            return "Deposit Successfully\n-----------------\n";
        }
        return "Sorry, The Amount Must Be Greater Than 0\n-----------------\n";
    }
    string withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            return "Withdraw Successfully\n-----------------\n";
        }
        return "Sorry, The Amount Was 0 or Less or The Amount Greater Than balance\n-----------------\n";
    }
    string transfer(Account& receiver, double amount) {
        if (this == &receiver) {
            return "Transfer Error\n-----------------\n";
        }
        else if (amount > 0 && amount <= this->balance) {
            receiver.deposit(amount);
            this->withdraw(amount);
            return "Transfer Successfully\n-----------------\n";
        }
        return "Transfer Error\n-----------------\n";
    }
};

class Bank {
private:
    vector<Account> accounts;
    vector<int> numbers;
public:
    string AddAccount(Account &account) {
        if (find(numbers.begin(), numbers.end(), account.getNumber()) != numbers.end()) {
            return "Sorry, This Number Was Taken\n-----------------\n";
        }
        accounts.push_back(account);
        numbers.push_back(account.getNumber());
        return "";
    }
    string AccountFind(int number) {
        for (int i = 0; i < accounts.size(); i++) {
            if (number == accounts[i].getNumber()) {
                return "\nAccount Found:\n- Account Name: " + accounts[i].getName()
                + "\n- Account Balance: " + to_string(accounts[i].getBalance()) + "\n-----------------";
            }
        }
        return "\nAccount Not Found\n-----------------\n";
    }
    string DeleteAccount(int number) {
        for (int i = 0; i < accounts.size(); i++) {
            if (accounts[i].getNumber() == number) {
                accounts.erase(accounts.begin() + i);
                numbers.erase(find(numbers.begin(), numbers.end(), number));
                return "Account Deleted Successfully\n-----------------\n";
            }
        }
        return "\nAccount Not Found\n-----------------\n";
    }
    string AccountsCount() {
        int count = 0;
        for (int i = 0; i < accounts.size(); i++) {
            count += 1;
        }
        return to_string(count) + "\n-----------------\n";
    }
    string transfer_between_accounts(int sender_number, int receiver_number, double amount) {
        if (sender_number != receiver_number) {
            Account* sender = nullptr;
            Account* receiver = nullptr;
            bool sender_exists = false, receiver_exists = false;
            for (int i = 0; i < accounts.size(); i++) {
                if (accounts[i].getNumber() == sender_number) {
                    sender = &accounts[i];
                    sender_exists = true;
                }
                else if (accounts[i].getNumber() == receiver_number) {
                    receiver = &accounts[i];
                    receiver_exists = true;
                }
            }
            if (sender_exists && receiver_exists) {
                sender->transfer(*receiver, amount);
                return "Transfer Successfully\n-----------------\n";
            }
            return "Account/Accounts Not Found\n-----------------\n";
        }
        return "Error, Sender Number and Reciver Number is Equal\n-----------------\n";
    }
};
int main() {
    Bank myBank;
    Account acc1("Ahmed", 101, 1000);
    Account acc2("Sara", 102, 500);
    cout << myBank.AddAccount(acc1);
    cout << myBank.AddAccount(acc2);

    cout << acc1.transfer(acc2, 300);

    cout << myBank.AccountFind(101);
    cout << myBank.AccountFind(102);
    return 0;
}
