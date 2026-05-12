using System;

namespace Lab3
{
    public class BankAccount
    {
        private static int _total = 0;
        private decimal _balance;

        // Використовуємо автоматичну властивість get та readonly поле
        public string AccountNumber { get; } 
        public string Owner { get; set; }
        public decimal Balance => _balance; // Скорочений get

        // Основний конструктор (використовуємо значення за замовчуванням для балансу)
        public BankAccount(string number, string owner, decimal balance = 0)
        {
            AccountNumber = number;
            Owner = owner;
            _balance = balance;
            _total++;
        }

        public static int GetTotal() => _total;

        public void Deposit(decimal amount) => _balance += amount > 0 ? amount : 0;

        public bool Withdraw(decimal amount)
        {
            if (amount <= 0 || _balance < amount) return false;
            _balance -= amount;
            return true;
        }

        public override string ToString() => $"[{AccountNumber}] {Owner}: {Balance:C}";
    }

    class Program
    {
        static void Main()
        {
            Console.OutputEncoding = System.Text.Encoding.UTF8;

            var acc1 = new BankAccount("UA001", "Шевченко", 1000);
            var acc2 = new BankAccount("UA002", "Коваленко"); // Баланс 0 за замовчуванням

            acc1.Withdraw(200);
            acc2.Deposit(500);

            Console.WriteLine(acc1);
            Console.WriteLine(acc2);
            Console.WriteLine($"Всього рахунків: {BankAccount.GetTotal()}");
        }
    }
}
