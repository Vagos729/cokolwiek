/******************************************************************************
                            Program wykonali:
                            Damian Stańczyk,
                            Jakub Włodarczyk
*******************************************************************************/

#include <iostream>
#include <vector>
#include <string>
#include <random>
#include <algorithm>

struct Osoba {
    std::string imie;
    std::string nazwisko;
    int data_urodzenia;
    
    Osoba(std::string imie, std::string nazwisko, int data_urodzenia) {
        this->imie = imie;
        this->nazwisko = nazwisko;
        this->data_urodzenia = data_urodzenia;
    }
};

std::vector<Osoba> wygeneruj_losowe_osoby(int count) {
    std::vector<Osoba> osoby;
    std::vector<std::string> imiona = {"Michal", "Jakub", "Kacper", "Filip", "Wojciech", "Szymon", "Antoni", "Damian", "Gracjan", "Aleksander"};
    std::vector<std::string> nazwiska = {"Nowak", "Kowalski", "Wisniewski", "Kwiatkowski", "Lewandowski", "Mazurkiewicz", "Piotrkowski", "Adamowicz", "Andrzejewski", "Baranowski"};
    srand(time(0));

    for (int i = 0; i < count; i++) {
        int imie_index = rand() % imiona.size();
        int nazwisko_index = rand() % nazwiska.size();
        int data_urodzenia = rand() % 50 + 1970;
        osoby.push_back(Osoba(imiona[imie_index], nazwiska[nazwisko_index], data_urodzenia));
    }

    return osoby;
}

void display_osoby(const std::vector<Osoba>& osoby) {
    for (const auto& osoby : osoby) {
        std::cout << osoby.imie << " " << osoby.nazwisko << ", " << osoby.data_urodzenia << std::endl;
    }
}

void sort_osoby_by_imie(std::vector<Osoba>& osoby) {
    std::sort(osoby.begin(), osoby.end(), [](const Osoba& a, const Osoba& b) {
        return a.imie < b.imie;
    });
}

void sort_osoby_by_nazwisko(std::vector<Osoba>& osoby) {
    std::sort(osoby.begin(), osoby.end(), [](const Osoba& a, const Osoba& b) {
        return a.nazwisko < b.nazwisko;
    });
}

void sort_osoby_by_data_urodzenia(std::vector<Osoba>& osoby) {
    std::sort(osoby.begin(), osoby.end(), [](const Osoba& a, const Osoba& b) {
        return a.data_urodzenia < b.data_urodzenia;
    });
}

int main() {
    int osoby_count;
    std::cout << "Podaj liczbe osob do wygenerowania: ";
    std::cin >> osoby_count;

    std::vector<Osoba> osoby = wygeneruj_losowe_osoby(osoby_count);
    display_osoby(osoby);

    int choice;
    std::cout << "Jak chcesz posortowac liste? (1 - po imieniu, 2 - po nazwisku, 3 - po dacie urodzenia): ";
    std::cin >> choice;

    switch (choice) {
        case 1:
            sort_osoby_by_imie(osoby);
            break;
        case 2:
            sort_osoby_by_nazwisko(osoby);
            break;
        case 3:
            sort_osoby_by_data_urodzenia(osoby);
            break;
        default:
            std::cout << "Nieprawidlowy wybor" << std::endl;
            break;
    }

    std::cout << "Posortowana lista:" << std::endl;
    display_osoby(osoby);

    return 0;
}