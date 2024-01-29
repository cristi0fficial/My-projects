#include <iostream>
#include <vector>
#include <algorithm> 
#include <string>
using namespace std;
class Book {
public:
Book(string title, string author, string isbn):title(title), author(author), isbn(isbn) {}
    string getTitle() const { return title; }
    string getAuthor() const { return author; }
    string getISBN() const { return isbn; }
private:
    string title;
    string author;
    string isbn;
};
class Library {
public:
  
    void addBook(const Book& book) {
        books.push_back(book);
    }

    
    void removeBook(const string& isbn) {
        auto it =remove_if(books.begin(), books.end(),
        [&isbn](const Book& book) { return book.getISBN() == isbn; });

        if (it != books.end()) {
            books.erase(it, books.end());
            cout << "Book with ISBN " << isbn << " removed from the library.\n";
        } else {
            cout << "Book with ISBN " << isbn << " not found in the library.\n";
        }
    }    
 
    void displayBooks() const {
        if (books.empty()) {
        cout << "Library is empty.\n";
        } else {
        cout << "Books in the library:\n";
        for (const auto& book : books) {
        cout << "Title: " << book.getTitle() << ", Author: " << book.getAuthor() << ", ISBN: " << book.getISBN() << "\n";
            }
        }
    }

private:
 
vector<Book> books;
};

int main() {
    Library library;
 
    library.addBook(Book("The Catcher in the Rye", "J.D. Salinger", "978-0-316-76948-0"));
    library.addBook(Book("To Kill a Mockingbird", "Harper Lee", "978-0-06-112008-4"));
    library.addBook(Book("1984", "George Orwell", "978-0-452-28423-4"));

    library.displayBooks();

    library.removeBook("978-0-06-112008-4");

    library.displayBooks();

    return 0;
}


