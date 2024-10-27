#include <iostream>
#include <vector>
#include <string>
#include <limits> // Include this header for std::numeric_limits

class Vehicle {
public:
    Vehicle(const std::string& brand, const std::string& model, int year)
        : brand(brand), model(model), year(year) {}

    void displayInfo() const {
        std::cout << "Brand: " << brand 
                  << ", Model: " << model 
                  << ", Year: " << year << std::endl;
    }

private:
    std::string brand;
    std::string model;
    int year;
};

class VehicleManagementSystem {
public:
    void addVehicle(const std::string& brand, const std::string& model, int year) {
        vehicles.emplace_back(brand, model, year);
        std::cout << "Vehicle added successfully!" << std::endl;
    }

    void viewVehicles() const {
        if (vehicles.empty()) {
            std::cout << "No vehicles in the system." << std::endl;
            return;
        }
        std::cout << "Vehicles in the system:" << std::endl;
        for (const auto& vehicle : vehicles) {
            vehicle.displayInfo();
        }
    }

    void removeVehicle(int index) {
        if (index < 0 || index >= vehicles.size()) {
            std::cout << "Invalid index." << std::endl;
            return;
        }
        vehicles.erase(vehicles.begin() + index);
        std::cout << "Vehicle removed successfully!" << std::endl;
    }

private:
    std::vector<Vehicle> vehicles;
};

int main() {
    VehicleManagementSystem vms;
    int choice;

    do {
        std::cout << "\nVehicle Management System" << std::endl;
        std::cout << "1. Add Vehicle" << std::endl;
        std::cout << "2. View Vehicles" << std::endl;
        std::cout << "3. Remove Vehicle" << std::endl;
        std::cout << "4. Exit" << std::endl;
        std::cout << "Enter your choice: ";
        std::cin >> choice;
        std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');  // Ignore remaining input in the line

        switch (choice) {
            case 1: {
                std::string brand, model;
                int year;
                std::cout << "Enter brand: ";
                std::getline(std::cin, brand);
                std::cout << "Enter model: ";
                std::getline(std::cin, model);
                std::cout << "Enter year: ";
                std::cin >> year;
                std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');  // Ignore remaining input
                vms.addVehicle(brand, model, year);
                break;
            }
            case 2:
                vms.viewVehicles();
                break;
            case 3: {
                int index;
                std::cout << "Enter vehicle index to remove: ";
                std::cin >> index;
                vms.removeVehicle(index);
                break;
            }
            case 4:
                std::cout << "Exiting..." << std::endl;
                break;
            default:
                std::cout << "Invalid choice. Please try again." << std::endl;
        }
    } while (choice != 4);

    return 0; // Corrected return statement
}
