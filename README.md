# -FoodProduct-

 Атрибуты класса
Для класса `FoodProduct` мы выберем следующие поля:
Название продукта (строка)
Цена(вещественное число)
Количество калорий (целое число)
Срок годности (строка)


 добавим метод, который будет возвращать статус продукта в зависимости от его срока годности: "Свежий", "Скоро истечет" или "Испорчен".


```cpp
#include <iostream>
#include <string>
#include <vector>
#include <algorithm> // Для сортировки
using namespace std;

class FoodProduct {
private:
    string name;          // Название продукта
    float price;          // Цена продукта
    int calories;         // Количество калорий
    string expirationDate; // Срок годности

public:
    // Конструктор по умолчанию
    FoodProduct() : name("Unknown"), price(0.0), calories(0), expirationDate("Unknown") {}

    // Конструктор с параметрами
    FoodProduct(string n, float p, int c, string e) : name(n), price(p), calories(c), expirationDate(e) {}

    // Методы доступа
    string getName() const { return name; }
    float getPrice() const { return price; }
    int getCalories() const { return calories; }
    string getExpirationDate() const { return expirationDate; }

    void setName(string n) { name = n; }
    void setPrice(float p) { price = p; }
    void setCalories(int c) { calories = c; }
    void setExpirationDate(string e) { expirationDate = e; }

    // Метод для получения статуса продукта на основе срока годности
    string getStatus() const {
        // Простой пример статуса, можно доработать в зависимости от формата даты
        if (expirationDate == "Fresh") return "Fresh";
        else if (expirationDate == "Soon") return "Soon to expire";
        else return "Expired";
    }

    // Метод для вывода информации о продукте
    void display() const {
        cout << "Name: " << name << ", Price: $" << price << ", Calories: " << calories
             << ", Expiration Date: " << expirationDate << ", Status: " << getStatus() << endl;
    }
};

// Функция для отображения меню
void displayMenu() {
    cout << "Menu:" << endl;
    cout << "1. Add empty product" << endl;
    cout << "2. Add product with data" << endl;
    cout << "3. Edit product data" << endl;
    cout << "4. Display all products" << endl;
    cout << "5. Sort products by price" << endl;
    cout << "6. Exit" << endl;
}

int main() {
    vector<FoodProduct> products; // Массив объектов FoodProduct
    int choice;

    do {
        displayMenu();
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
            case 1: { // Добавление пустого продукта
                products.push_back(FoodProduct());
                cout << "Empty product added." << endl;
                break;
            }
            case 2: { // Добавление продукта с данными
                string name, expirationDate;
                float price;
                int calories;
                cout << "Enter name: ";
                cin >> name;
                cout << "Enter price: ";
                cin >> price;
                cout << "Enter calories: ";
                cin >> calories;
                cout << "Enter expiration date (Fresh, Soon, Expired): ";
                cin >> expirationDate;
                products.push_back(FoodProduct(name, price, calories, expirationDate));
                cout << "Product added." << endl;
                break;
            }
            case 3: { // Редактирование данных продукта
                int index;
                cout << "Enter product index to edit (0 to " << products.size() - 1 << "): ";
                cin >> index;
                if (index >= 0 && index < products.size()) {
                    string name, expirationDate;
                    float price;
                    int calories;
                    cout << "Enter new name: ";
                    cin >> name;
                    cout << "Enter new price: ";
                    cin >> price;
                    cout << "Enter new calories: ";
                    cin >> calories;
                    cout << "Enter new expiration date (Fresh, Soon, Expired): ";
                    cin >> expirationDate;
                    products[index].setName(name);
                    products[index].set
                    products[index].setPrice(price);
                    products[index].setCalories(calories);
                    products[index].setExpirationDate(expirationDate);
                    cout << "Product updated." << endl;
                } else {
                    cout << "Invalid index." << endl;
                }
                break;
            }
            case 4: { // Вывод информации обо всех продуктах
                if (products.empty()) {
                    cout << "No products available." << endl;
                } else {
                    for (const auto& product : products) {
                        product.display();
                    }
                }
                break;
            }
            case 5: { // Сортировка продуктов по цене
                if (products.empty()) {
                    cout << "No products to sort." << endl;
                } else {
                    sort(products.begin(), products.end(), [](const FoodProduct& a, const FoodProduct& b) {
                        return a.getPrice() < b.getPrice();
                    });
                    cout << "Products sorted by price." << endl;
                }
                break;
            }
            case 6: // Завершение работы программы
                cout << "Exiting program." << endl;
                break;
            default:
                cout << "Invalid choice. Please try again." << endl;
        }
    } while (choice != 6);

    return 0;
}
```
