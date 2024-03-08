package codsoft.Internship;

import java.util.Scanner;
 class BankAccount {
     private double accountBalance;
     public BankAccount(double intialBalance){
         this.accountBalance = intialBalance;
     }
     public boolean depositFunds(double amount){
         if(amount > 0){
             this.accountBalance += amount;
             return true;
         } else{
             System.out.println("Invalid deposit amount.");
             return  false;
         }
     }
     public boolean withdrawFunds(double amount){
         if (amount >0 && amount <= this.accountBalance){
             this.accountBalance -= amount;
             return true;
         } else{
             System.out.println("Invalid withdrawal amount or insufficient funds.");
             return false;
         }
     }
     public double checkAccountBalance(){return this.accountBalance;}
 }
 class AutomatedTellerMachine {
     private BankAccount bankAccount;
     public AutomatedTellerMachine(BankAccount bankAccount){ this.bankAccount = bankAccount;}

     public void displayMenu(){
         System.out.println("1.withdrawal Funds");
         System.out.println("2. Deposit Funds");
         System.out.println("3. Check Account Balance");
         System.out.println("4. Exit");
     }
     public void operateATM() {
         Scanner scanner = new Scanner(System.in);

         while(true) {
             displayMenu();
             System.out.println("Enter your choice (1-4): ");
             int choice = scanner.nextInt();

             switch (choice) {
                 case 1:
                     System.out.println("Enter the amount to withdrawal: ");
                     double withdrawAmount = scanner.nextDouble();
                     if(bankAccount.withdrawFunds(withdrawAmount)){
                         System.out.println("Withdrawal successful. Remaining balance: " + bankAccount.checkAccountBalance());
                     }
                     break;
                 case 2:
                     System.out.println("Enter the amount to deposit: ");
                     double depositAmount = scanner.nextDouble();;
                     bankAccount.depositFunds(depositAmount);
                     System.out.println("Deposit successful.Current balance: " + bankAccount.checkAccountBalance());
                     break;
                 case 3:
                     System.out.println("Current account balance: " + bankAccount.checkAccountBalance());
                     break;
                 case 4:
                     System.out.println("Existing ATM. Thank You!");
                     scanner.close();
                     System.exit(0);

                 default:
                     System.out.println("Invalid choice.Please enter a number between 1 and 4.");
                     break;
             }
         }
     }
 }

public class ATM_Interface {
    public static void main(String[] args) {
        BankAccount bankAccount = new BankAccount(1000);
        AutomatedTellerMachine atm = new AutomatedTellerMachine(bankAccount);
        atm.operateATM();
    }
}
