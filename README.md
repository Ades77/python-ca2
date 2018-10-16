# python-ca2
from operator import methodcaller
import datetime
today = datetime.datetime.now()

current_year = today.year


class LibraryItem:
    def __init__(self, id, title, pubyear):
        self.__id = id
        self.__title = title
        self.__pubyear = pubyear

    def __str__(self):
        return 'Library Item, ID: {}, Title: {}, Year of Publication: {}'.format\
        (self.__id, self.__title, self.__pubyear)

    def print_details(self):
        print('Library Item')
        print('ID:', self.__id)
        print('Title:', self.__title)
        print('Year of Publication:', self.__pubyear)
        print('')

    def get_id(self):
        return self.__id

    def get_title(self):
        return self.__title

    def get_pubyear(self):
        return self.__pubyear


class Book(LibraryItem):
    def __init__(self, id, title, pubyear, author, isbn):
        LibraryItem.__init__(self, id, title, pubyear)
        self.__id = id
        self.__title = title
        self.__pubyear = pubyear
        self.__author = author
        self.__isbn = isbn

    def __str__(self):
        return 'Book, ID: {},  Title: {}, Year of Publication: {}, Author: {}, ISBN: {}'.format\
        (self.__id, self.__title, self.__pubyear, self.__author, self.__isbn)

    def print_details(self):
        print('Book')
        print('ID:', self.__id)
        print('Title:', self.__title)
        print('Year of Publication:', self.__pubyear)
        print('Author:', self.__author)
        print('ISBN:', self.__isbn)
        print('')

    def get_author(self):
        return self.__author

    def get_isbn(self):
        return self.__isbn


class Periodical(LibraryItem):
    def __init__(self, id, title, pubyear, editor, volume, issue):
        LibraryItem.__init__(self, id, title, pubyear)
        self.__id = id
        self.__title = title
        self.__pubyear = pubyear
        self.__editor = editor
        self.__volume = volume
        self.__issue = issue

    def __str__(self):
        return 'Periodical, ID: {}, Title: {}, Year of Publication: {}, Editor: {}, Volume: {}, Issue: {}'.format\
        (self.__id, self.__title, self.__pubyear, self.__editor, self.__volume, self.__issue)

    def print_details(self):
        print('Periodical')
        print('ID:', self.__id)
        print('Title:', self.__title)
        print('Year of Publication:', self.__pubyear)
        print('Editor:', self.__editor)
        print('Volume:', self.__volume)
        print('Issue:', self.__issue)
        print('')

    def get_editor(self):
        return self.__editor

    def get_volume(self):
        return self.__volume

    def get_issue(self):
        return self.__issue


class User:
    def __init__(self, id, name, address):
        self.__id = id
        self.__name = name
        self.__address = address
        self.__loans = []

    def __str__(self):
        return 'User, ID: {}, Name: {}, Address: {}, Books on loan: {}'.format\
        (self.__id, self.__name, self.__address, self.__loans)

    def print_details(self):
        print('User')
        print('ID:', self.__id)
        print('Name:', self.__name)
        print('Address:', self.__address)
        print('Books on loan:', self.__loans)
        print('')

    def get_id(self):
        return self.__id

    def get_name(self):
        return self.__name

    def get_address(self):
        return self.__address

    def add_loan(self, title):
        """Adds the title of a book that has been loaned to the list of loaned books associated with the user"""
        self.__loans.append(title)

    def remove_loan(self, title):
        """Removes the title of a book that was loaned and has now been returned from the list of loaned books"""
        self.__loans.remove(title)

    def get_loan_titles(self):
        """Returns the list of books that the user has on loan"""
        return self.__loans


b1 = Book(7, 'Jump', 2000, 'Jane Doe', 1111111111111)  # small library to initiate program
b2 = Book(1, 'Jump', 2003, 'Jane Doe', 1111111111111)
b3 = Book(2, 'Hello', 1991, 'John Doe', 2222222222222)
p1 = Periodical(5, 'Period1', 1996, 'Jack Smith', 6, 32)
p2 = Periodical(3, 'Period2', 2008, 'Amy Small', 3, 16)
u1 = User(3, 'John Bass', '4 Suncroft Drive')
u2 = User(4, 'Anna Leonard', '5 The Hilltop')
u3 = User(1, 'James Smith', '9 The Meadow')
library_items = [b1, b2, b3, p1, p2]  # list of library items, every item in the library is added to this list
book_list = [b1, b2, b3]  # list of books in the library
periodical_list = [p1, p2]  # list of periodicals in the library
user_list = [u1, u2, u3]  # list of users in the system
loaned_books = []  # list of books out on loan
available_books = [b1, b2, b3]  # list of books available for loan


def title_search(title):
    """Allows the user to search for a library item by title"""
    count = 0
    flag = 0
    for item in library_items:  # iterates over the objects in the list of library items
        count += 1
        if title.lower() == item.get_title().lower():  # accesses the title for each object in the list and
            # compares it to the title entered by the user in lowercase
            item.print_details()
            flag = 1
    if flag == 0 and count == len(library_items):
        print('There are no items with that title in the library.')


def pubyear_search(pubyear):
    """Allows the user to search for a library item by year of publication"""
    count = 0
    flag = 0
    for item in library_items:
        count += 1
        if pubyear == item.get_pubyear():
            item.print_details()
            flag = 1
    if flag == 0 and count == len(library_items):
        print('There are no items with that year of publication in the library.')


def id_search(id):
    """Allows the user to search for a library item by ID"""
    count = 0
    flag = 0
    for item in library_items:
        count += 1
        if id == item.get_id():
            item.print_details()
            flag = 1
    if flag == 0 and count == len(library_items):
        print('There is no item with that ID in the library.')


def author_search(author):
    """Allows the user to search for a book by author"""
    count = 0
    flag = 0
    for item in book_list:
        count += 1
        if author.lower() == item.get_author().lower():
            item.print_details()
            flag = 1
    if flag == 0 and count == len(book_list):
        print('There are no books by that author in the library.')


def isbn_search(isbn):
    """Allows the user to search for a book by ISBN"""
    count = 0
    flag = 0
    for item in book_list:
        count += 1
        if isbn == item.get_isbn():
            item.print_details()
            flag = 1
    if flag == 0 and count == len(book_list):
        print('There are no books with that ISBN in the library.')


def editor_search(editor):
    """Allows the user to search for a periodical by editor"""
    count = 0
    flag = 0
    for item in periodical_list:
        count += 1
        if editor.lower() == item.get_editor().lower():
            item.print_details()
            flag = 1
    if flag == 0 and count == len(periodical_list):
        print('There are no periodicals by that editor in the library.')


def userid_search(userid):
    """Allows the user to search for a user by ID"""
    count = 0
    flag = 0
    for item in user_list:
        count += 1
        if userid == item.get_id():
            item.print_details()
            flag = 1
    if flag == 0 and count == len(user_list):
        print('There is no user with that ID in the system.')


def name_search(name):
    """Allows the user to search for a user by name"""
    count = 0
    flag = 0
    for item in user_list:
        count += 1
        if name.lower() == item.get_name().lower():
            item.print_details()
            flag = 1
    if flag == 0 and count == len(user_list):
        print('There are no users with that name in the system.')


def address_search(address):
    """Allows the user to search for a user by address"""
    count = 0
    flag = 0
    for item in user_list:
        count += 1
        if address.lower() == item.get_address().lower():
            item.print_details()
            flag = 1
    if flag == 0 and count == len(user_list):
        print('There are no users with that address in the system.')


def borrow_book(isbn, userid):
    """Allows the user to borrow a book from the library only if the user is in the system"""
    flag_a = 0
    count_a = 0
    for items in user_list:
        count_a += 1
        if items.get_id() == userid:  # if the user is in the system
            user = items
            flag_a += 1
            flag_b = 0
            count_b = 0
            for item in available_books:  # if the book is available for loaning
                count_b += 1
                if isbn == item.get_isbn():  # if the book is in the library(isbn present)
                    loaned_books.append(item)  # add the book to list of loaned books
                    available_books.remove(item)  # remove the book from list of available books
                    print(item.get_title(), 'borrowed.')
                    flag_b += 1
                    user.add_loan(item.get_title())  # add the book title to the user's list of loaned books
                    break  # break so that the user can only borrow 1 copy of that book if multiples are present
                elif flag_b == 0 and len(available_books) == count_b:
                    print('Item not available for loan.')
            if len(available_books) == 0:
                print('No items available for loan.')
        elif flag_a == 0 and len(user_list) == count_a:
            print('User not in system, unable to borrow book.')
    if len(user_list) == 0:
        print('No users in the system, add users to borrow books.')


def return_book(bookid, userid):
    """Allows the user to return a book to the library that they have borrowed"""
    flag_a = 0
    count_a = 0
    if len(loaned_books) == 0:
        print('No books are out on loan.')
    for items in user_list:
        count_a += 1
        if items.get_id() == userid:
            user = items
            flag_a += 1
            count = 0
            for item in loaned_books:
                count += 1
                if bookid == item.get_id() and item.get_title() in user.get_loan_titles():  # if book ID entered is in
                    # the list of loaned books and the book title is in the user's list of loaned books
                    loaned_books.remove(item)  # remove the book from list of loaned books
                    available_books.append(item)  # return the book to list of available books
                    user.remove_loan(item.get_title())  # remove the book title from user's list of loaned books
                    print(item.get_title(), 'returned.')
                    break  # break so that if user has more than 1 copy of same book loaned out, only 1 is returned
                elif bookid != item.get_id() and count == len(loaned_books):
                    print('Sorry, that item was not loaned out.')
                elif bookid == item.get_id() and item.get_title() not in user.get_loan_titles():
                    print('That book was not loaned out by that user.')
        elif flag_a == 0 and len(user_list) == count_a:
            print('User not in system, unable to return book.')
    if len(user_list) == 0:
        print('No users in the system, add users to return books.')


def add_user(id, name, address):
    user = User(id, name, address)
    user_list.append(user)
    print('User', name, 'added to the library.')


def delete_user(id):
    """Allows the user to remove a user from the system"""
    id_found = 0
    for item in user_list:
        if item.get_id() == id:
            id_found = id
            print('Do you want to remove the user', item.get_name(), 'with ID', id, '?')
            choice = input('Enter yes or no.')
            if choice == 'yes' or choice == 'y':
                user_list.remove(item)
                print('The user', item.get_name(), 'with ID', id, 'has been removed.')
            elif choice == 'no' or choice == 'n':
                print('The user', item.get_name(), 'with ID', id, 'was not removed.')
            else:
                print('Invalid input.')
    if id_found != id:
        print('There is no user with that ID in the system.')


def add_book(isbn):
    """Allows the user to add a book to the library"""
    count = 0
    for item in book_list:
        count += 1
        if isbn == item.get_isbn():  # if book is already in the library(isbn present)
            print('Title:', item.get_title())
            print('Author:', item.get_author())
            print('')
            print('This ISBN is already in the library, details of the book have been printed. '
                  'Do you want to add another entry of this book to the library? '
                  'Only year of publication can be updated.')
            choice = input('Enter yes or no')
            if choice == 'yes' or choice == 'y':
                pubyear = pubyear_check()
                id = valid_item_id()  # calls functions to ask for input for id and pubyear and check for validity
                book = Book(id, item.get_title(), pubyear, item.get_author(), isbn)  # adds a new entry of that book
                # with new valid ID and pubyear input from user, other fields remain the same as before,
                # cannot change author or book title
                library_items.append(book)
                book_list.append(book)
                available_books.append(book)
                print(item.get_title(), 'added to the library.')
                break
            elif choice == 'no' or choice == 'n':
                print('A new entry of that book was not added to the library.')
                break
            else:
                print('Invalid choice')
        elif isbn != item.get_isbn() and count == len(book_list):  # if isbn not in the library, can add a new book
            id = valid_item_id()
            title = input('Enter the title of the book you want to add.')
            pubyear = pubyear_check()
            author = input('Enter the author of the book you want to add.')
            book = Book(id, title, pubyear, author, isbn)
            library_items.append(book)
            book_list.append(book)
            available_books.append(book)
            print(title, 'added to the library.')
            break


def delete_library_item(id):
    """Allows the user to remove a library item from the library"""
    id_found = 0
    for item in library_items:
        if item.get_id() == id:
            id_found = id
            if type(item) == Book and item in loaned_books:  # if item is a book and is loaned out
                print('That book cannot be removed as it is on loan.')
            elif type(item) == Book:  # if the item is a Book object
                print('Do you want to remove the book', item.get_title(), 'with ID', id, '?')
                choice = input('Enter yes or no.')
                if choice == 'yes' or choice == 'y':
                    book_list.remove(item)  # remove the object from the list of books
                    available_books.remove(item)  # remove the object from the list of books that can be loaned out
                    library_items.remove(item)  # remove the object from the list of library items
                    print('The book', item.get_title(), 'with ID', id, 'has been removed.')
                elif choice == 'no' or choice == 'n':
                    print('The book', item.get_title(), 'with ID', id, 'was not removed.')
                else:
                    print('Invalid input.')
            elif type(item) == Periodical:
                print('Do you want to remove the periodical', item.get_title(), 'with ID', id, '?')
                choice = input('Enter yes or no.')
                if choice == 'yes' or choice == 'y':
                    periodical_list.remove(item)  # remove the object from the list of periodicals
                    library_items.remove(item)
                    print('The periodical', item.get_title(), 'with ID', id, 'has been removed.')
                elif choice == 'no ' or choice == 'n':
                    print('The periodical', item.get_title(), 'with ID', id, 'was not removed.')
                else:
                    print('Invalid input.')
    if id_found != id:
        print('There is no item with that ID in the library.')


def add_periodical(id, title, pubyear, editor, volume, issue):
    periodical = Periodical(id, title, pubyear, editor, volume, issue)
    library_items.append(periodical)
    periodical_list.append(periodical)
    print(title, 'added to the library.')


def available_book_check(isbn):
    """Allows the user to check if a book is available for loan"""
    count = 0
    flag = 0
    for item in available_books:
        count += 1
        if item.get_isbn() == isbn:
            print(item.get_title(), 'is available for loan.')
            flag = 1
            break
    if flag == 0 and count == len(available_books):
        print('Sorry, that book is not available for loan.')


def isbn_check():
    """Checks that input from user for ISBN is a 13 digit number"""
    try:  # checks that ISBN is a number
        isbn = int(input('Enter the ISBN of the book.'))
        if len(str(isbn)) != 13 or isbn < 0:  # checks that ISBN is 13 digits and positive
            print('ISBN must be a 13 digit number.')
            isbn = isbn_check()
    except ValueError:
        print('ISBN must be a number.')
        isbn = isbn_check()
    return isbn


def pubyear_check():
    """Checks that input from user for pubyear is a number and not larger than current year"""
    try:  # checks that pubyear is a number
        pubyear = int(input('Enter the year of publication for the library item.'))
        if pubyear < 1 or pubyear > current_year:  # checks that pubyear is a valid date
            print('Year of publication must be a valid year.')
            pubyear = pubyear_check()
    except ValueError:
        print('Year of publication must be a number.')
        pubyear = pubyear_check()
    return pubyear


def item_id_check():
    """Checks that input from the user for item ID is a positive number"""
    try:  # checks that id is a number
        id = int(input('Enter the item ID.'))
        if id < 1:  # checks if number entered is positive
            print('The ID entered must be a positive number.')
            id = item_id_check()
    except ValueError:
        print('ID must be a number.')
        id = item_id_check()
    return id


def user_id_check():
    """Checks that input from the user for user ID is a positive number"""
    try:  # checks that id is a number
        id = int(input('Enter the user ID.'))
        if id < 1:  # checks if number entered is positive
            print('The ID entered must be a positive number.')
            id = user_id_check()
    except ValueError:
        print('ID must be a number.')
        id = user_id_check()
    return id


def valid_item_id():
    """Checks that input from user for item ID is not already in the system"""
    try:  # checks that id is a number
        id = int(input('Enter the item ID.'))
        id_found = 0
        for item in library_items:
            if item.get_id() == id:
                id_found = id
        if id_found == id:
            print('That ID is already in the library, please enter a different ID.')
            id = valid_item_id()
            return id
    except ValueError:
        print('ID must be a number.')
        id = valid_item_id()
    return id


def valid_user_id():
    """Checks that input from user for user ID is not already in the system"""
    try:  # checks that id is a number
        id = int(input('Enter the user ID.'))
        id_found = 0
        for item in user_list:
            if item.get_id() == id:
                id_found = id
        if id_found == id:
            print('That user ID is already in the system, please enter a different ID.')
            id = valid_user_id()
            return id
    except ValueError:
        print('ID must be a number.')
        id = valid_user_id()
    return id


def volume_check():
    """Checks that input from user for volume is a positive number"""
    try:  # checks that volume is a number
        volume = int(input('Enter the volume number.'))
        if volume < 1:  # checks if number entered is positive
            print('The volume entered must be a positive number.')
            volume = volume_check()
    except ValueError:
        print('Volume must be a number.')
        volume = volume_check()
    return volume


def issue_check():
    """Checks that input from user for issue is a positive number"""
    try:  # checks that copies is a number
        issue = int(input('Enter the issue number.'))
        if issue < 1:  # checks if number entered is positive
            print('The issue entered must be a positive number.')
            issue = issue_check()
    except ValueError:
        print('Issue must be a number.')
        issue = issue_check()
    return issue


def print_menu():
    print('****Library Catalogue****')
    print('')
    print('1. Print details about library items.')
    print('2. Print details about library users.')
    print('3. Print out all books on loan.')
    print('4. Add a book to the library.')
    print('5. Add a periodical to the library.')
    print('6. Add a user to the library.')
    print('7. Search for a library item by keyword - id, title, year of publication(pubyear), author, isbn or editor.')
    print('8. Search for a user by keyword - id, name or address.')
    print('9. Check if a book is available for loan, requires ISBN.')
    print('10. Borrow a book from the library, requires user ID and book ISBN.')
    print('11. Return a book to the library, requires book ID.')
    print('12. Remove an item from the library, requires item ID.')
    print('13. Remove a user from the library, requires user ID.')
    print('14. Print all menu options again.')
    print('0. Exit the library catalogue.')
    print('')


print_menu()
user_input = ''

while user_input != '0':  # menu keeps going until user inputs 0, calls function depending on number entered
    user_input = input('Input the number of the option you want followed by enter to use the catalogue. '
                       'Input 14 for menu options.')
    if user_input == '1':
        library_items = sorted(library_items, key=methodcaller('get_id'))  # sorts the list of library items by id
        for item in library_items:
            item.print_details()
        if len(library_items) == 0:
            print('No library items in the library')
    elif user_input == '2':
        user_list = sorted(user_list, key=methodcaller('get_id'))  # sorts the list of users by id
        for item in user_list:
            item.print_details()
        if len(user_list) == 0:
            print('No users in the library')
    elif user_input == '3':
        loaned_books = sorted(loaned_books, key=methodcaller('get_id'))
        for item in loaned_books:
            item.print_details()
        if len(loaned_books) == 0:
            print('No books out on loan.')
    elif user_input == '4':
        isbn = isbn_check()
        add_book(isbn)
    elif user_input == '5':
        id = valid_item_id()
        title = input('Enter the title of the periodical you want to add.')
        pubyear = pubyear_check()
        editor = input('Enter the editor of the periodical you want to add.')
        volume = volume_check()
        issue = issue_check()
        add_periodical(id, title, pubyear, editor, volume, issue)
    elif user_input == '6':
        id = valid_user_id()
        name = input('Enter the name of the user you want to add.')
        address = input('Enter the address of the user you want to add.')
        add_user(id, name, address)
    elif user_input == '7':
        choice = input('Enter the keyword you want to search for an item by(id, title, pubyear, author, isbn, editor).')
        if choice == 'id':
            id = item_id_check()
            id_search(id)
        elif choice == 'title':
            title = input('Enter the title of the library item.')
            title_search(title)
        elif choice == 'pubyear':
            pubyear = pubyear_check()
            pubyear_search(pubyear)
        elif choice == 'author':
            author = input('Enter the author of the library item.')
            author_search(author)
        elif choice == 'isbn':
            isbn = isbn_check()
            isbn_search(isbn)
        elif choice == 'editor':
            editor = input('Enter the editor of the library item.')
            editor_search(editor)
        else:
            print('Invalid keyword entered.')
    elif user_input == '8':
        choice = input('Enter the keyword you want to search for a user by(id, name, address).')
        if choice == 'id':
            id = user_id_check()
            userid_search(id)
        elif choice == 'name':
            name = input('Enter the name of the user.')
            name_search(name)
        elif choice == 'address':
            address = input('Enter the address of the user.')
            address_search(address)
        else:
            print('Invalid keyword entered.')
    elif user_input == '9':
        isbn = isbn_check()
        available_book_check(isbn)
    elif user_input == '10':
        userid = user_id_check()
        isbn = isbn_check()
        borrow_book(isbn, userid)
    elif user_input == '11':
        bookid = item_id_check()
        userid = user_id_check()
        return_book(bookid, userid)
    elif user_input == '12':
        id = item_id_check()
        delete_library_item(id)
    elif user_input == '13':
        id = user_id_check()
        delete_user(id)
    elif user_input == '14':
        print_menu()
    elif user_input == '0':
        print('Thank you for using the library catalogue.')
    else:
        print('Input invalid.')

