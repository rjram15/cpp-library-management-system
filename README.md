# cpp-library-management-system
A console-based Library Management System developed in C++ to manage books, members, and borrowing records using object-oriented programming concepts.
#include <iostream>
#include <string>
using namespace std;

class Book {
public:
    int id;
    string title;
    string author;
    bool issued;

    void addBook() {
        cout << "\nEnter Book ID: ";
        cin >> id;
        cin.ignore();

        cout << "Enter Book Title: ";
        getline(cin, title);

        cout << "Enter Author Name: ";
        getline(cin, author);

        issued = false;
    }

    void displayBook() {
        cout << "\nBook ID      : " << id;
        cout << "\nTitle        : " << title;
        cout << "\nAuthor       : " << author;
        cout << "\nStatus       : " << (issued ? "Issued" : "Available");
        cout << "\n---------------------------";
    }
};

class Library {
private:
    Book books[100];
    int totalBooks = 0;

public:
    void addBook() {
        if (totalBooks >= 100) {
            cout << "\nLibrary is full!";
            return;
        }

        books[totalBooks].addBook();
        totalBooks++;
        cout << "\nBook Added Successfully!\n";
    }

    void displayBooks() {
        if (totalBooks == 0) {
            cout << "\nNo Books Available.\n";
            return;
        }

        cout << "\n===== Library Books =====\n";

        for (int i = 0; i < totalBooks; i++) {
            books[i].displayBook();
        }
    }

    void searchByTitle() {
        if (totalBooks == 0) {
            cout << "\nNo Books Available.\n";
            return;
        }

        string searchTitle;
        cin.ignore();

        cout << "\nEnter Book Title: ";
        getline(cin, searchTitle);

        bool found = false;

        for (int i = 0; i < totalBooks; i++) {
            if (books[i].title == searchTitle) {
                books[i].displayBook();
                found = true;
            }
        }

        if (!found)
            cout << "\nBook Not Found!\n";
    }

    void searchByAuthor() {
        if (totalBooks == 0) {
            cout << "\nNo Books Available.\n";
            return;
        }

        string searchAuthor;
        cin.ignore();

        cout << "\nEnter Author Name: ";
        getline(cin, searchAuthor);

        bool found = false;

        for (int i = 0; i < totalBooks; i++) {
            if (books[i].author == searchAuthor) {
                books[i].displayBook();
                found = true;
            }
        }

        if (!found)
            cout << "\nNo Books Found for this Author!\n";
    }

    void issueBook() {
        if (totalBooks == 0) {
            cout << "\nNo Books Available.\n";
            return;
        }

        int bookId;
        string member;

        cout << "\nEnter Book ID to Issue: ";
        cin >> bookId;
        cin.ignore();

        cout << "Enter Member Name: ";
        getline(cin, member);

        for (int i = 0; i < totalBooks; i++) {
            if (books[i].id == bookId) {
                if (!books[i].issued) {
                    books[i].issued = true;
                    cout << "\nBook Issued Successfully to " << member << "!\n";
                } else {
                    cout << "\nBook Already Issued!\n";
                }
                return;
            }
        }

        cout << "\nBook ID Not Found!\n";
    }

    void returnBook() {
        if (totalBooks == 0) {
            cout << "\nNo Books Available.\n";
            return;
        }

        int bookId;

        cout << "\nEnter Book ID to Return: ";
        cin >> bookId;

        for (int i = 0; i < totalBooks; i++) {
            if (books[i].id == bookId) {
                if (books[i].issued) {
                    books[i].issued = false;
                    cout << "\nBook Returned Successfully!\n";
                } else {
                    cout << "\nThis Book Was Not Issued.\n";
                }
                return;
            }
        }

        cout << "\nBook ID Not Found!\n";
    }
};

int main() {
    Library lib;
    int choice;

    do {
        cout << "\n==============================";
        cout << "\n   LIBRARY MANAGEMENT SYSTEM";
        cout << "\n==============================";
        cout << "\n1. Add Book";
        cout << "\n2. Display All Books";
        cout << "\n3. Search Book by Title";
        cout << "\n4. Search Book by Author";
        cout << "\n5. Issue Book";
        cout << "\n6. Return Book";
        cout << "\n7. Exit";
        cout << "\n------------------------------";
        cout << "\nEnter Your Choice: ";
        cin >> choice;

        switch (choice) {
        case 1:
            lib.addBook();
            break;

        case 2:
            lib.displayBooks();
            break;

        case 3:
            lib.searchByTitle();
            break;

        case 4:
            lib.searchByAuthor();
            break;

        case 5:
            lib.issueBook();
            break;

        case 6:
            lib.returnBook();
            break;

        case 7:
            cout << "\nThank You for Using the Library Management System!\n";
            break;

        default:
            cout << "\nInvalid Choice! Please Try Again.\n";
        }

    } while (choice != 7);

    return 0;
}
