# Music-Playlist-Manager
DSA Mini Project using Circular Doubly Linked List

#include <iostream>
#include <string>
using namespace std;

struct Song {
    int id;
    string title, artist;
    Song* next;
    Song* prev;
};

Song* head = NULL;
Song* current = NULL;

void addSong() {
    Song* s = new Song;

    cout << "Enter Song ID: ";
    cin >> s->id;
    cin.ignore();

    cout << "Enter Song Title: ";
    getline(cin, s->title);

    cout << "Enter Artist Name: ";
    getline(cin, s->artist);

    if (head == NULL) {
        head = s;
        s->next = s;
        s->prev = s;
        current = s;
    } else {
        Song* last = head->prev;

        s->next = head;
        s->prev = last;
        last->next = s;
        head->prev = s;
    }

    cout << "Song added successfully!\n";
}

void displaySongs() {
    if (head == NULL) {
        cout << "Playlist is empty!\n";
        return;
    }

    Song* temp = head;

    cout << "\n--- MUSIC PLAYLIST ---\n";
    do {
        cout << "ID: " << temp->id
             << " | Title: " << temp->title
             << " | Artist: " << temp->artist << endl;

        temp = temp->next;
    } while (temp != head);
}

void nextSong() {
    if (current == NULL) {
        cout << "Playlist is empty!\n";
        return;
    }

    current = current->next;
    cout << "Now Selected: " << current->title << endl;
}

void previousSong() {
    if (current == NULL) {
        cout << "Playlist is empty!\n";
        return;
    }

    current = current->prev;
    cout << "Now Selected: " << current->title << endl;
}

void searchSong() {
    if (head == NULL) {
        cout << "Playlist is empty!\n";
        return;
    }

    int id;
    cout << "Enter Song ID to search: ";
    cin >> id;

    Song* temp = head;

    do {
        if (temp->id == id) {
            cout << "Song Found: " << temp->title
                 << " by " << temp->artist << endl;
            return;
        }
        temp = temp->next;
    } while (temp != head);

    cout << "Song not found!\n";
}

void removeSong() {
    if (head == NULL) {
        cout << "Playlist is empty!\n";
        return;
    }

    int id;
    cout << "Enter Song ID to remove: ";
    cin >> id;

    Song* temp = head;

    do {
        if (temp->id == id) {
            if (temp->next == temp) {
                head = NULL;
                current = NULL;
            } else {
                temp->prev->next = temp->next;
                temp->next->prev = temp->prev;

                if (head == temp)
                    head = temp->next;

                if (current == temp)
                    current = temp->next;
            }

            delete temp;
            cout << "Song removed successfully!\n";
            return;
        }

        temp = temp->next;
    } while (temp != head);

    cout << "Song not found!\n";
}

int main() {
    int choice;

    do {
        cout << "\n===== MUSIC PLAYLIST MANAGER =====\n";
        cout << "1. Add Song\n";
        cout << "2. Display Playlist\n";
        cout << "3. Next Song\n";
        cout << "4. Previous Song\n";
        cout << "5. Search Song\n";
        cout << "6. Remove Song\n";
        cout << "7. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
            case 1: addSong(); break;
            case 2: displaySongs(); break;
            case 3: nextSong(); break;
            case 4: previousSong(); break;
            case 5: searchSong(); break;
            case 6: removeSong(); break;
            case 7: cout << "Exiting program...\n"; break;
            default: cout << "Invalid choice!\n";
        }

    } while (choice != 7);

    return 0;
}
