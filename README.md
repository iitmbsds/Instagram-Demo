# Instagram-Demo
Fully Operational Insta App Demo
AUTHOR : Bhaskar kumar
#include <iostream>
#include <vector>
#include <map>

using namespace std;

// User structure
struct User {
    string username;
    string password;
    vector<string> posts;
};

// Global variables
map<string, User> users;  // User database
User *currentUser = nullptr;

// Function to sign up
void signUp() {
    string username, password;
    cout << "Enter username: ";
    cin >> username;
    cout << "Enter password: ";
    cin >> password;

    if (users.find(username) == users.end()) {
        users[username] = {username, password, {}};
        cout << "Account created successfully!\n";
    } else {
        cout << "Username already exists!\n";
    }
}

// Function to log in
void logIn() {
    string username, password;
    cout << "Enter username: ";
    cin >> username;
    cout << "Enter password: ";
    cin >> password;

    if (users.find(username) != users.end() && users[username].password == password) {
        currentUser = &users[username];
        cout << "Login successful! Welcome, " << currentUser->username << "!\n";
    } else {
        cout << "Invalid credentials!\n";
    }
}

// Function to post an image (simulated)
void postImage() {
    if (!currentUser) {
        cout << "You need to log in first!\n";
        return;
    }

    string caption;
    cout << "Enter caption for your post: ";
    cin.ignore();
    getline(cin, caption);

    currentUser->posts.push_back(caption);
    cout << "Post uploaded successfully!\n";
}

// Function to view posts
void viewPosts() {
    if (!currentUser) {
        cout << "You need to log in first!\n";
        return;
    }

    cout << "Your Posts:\n";
    for (const string &post : currentUser->posts) {
        cout << "- " << post << endl;
    }
}

// Main function
int main() {
    int choice;
    while (true) {
        cout << "\nInstagram Demo\n";
        cout << "1. Sign Up\n2. Log In\n3. Post Image\n4. View Posts\n5. Exit\n";
        cout << "Enter choice: ";
        cin >> choice;

        switch (choice) {
            case 1: signUp(); break;
            case 2: logIn(); break;
            case 3: postImage(); break;
            case 4: viewPosts(); break;
            case 5: return 0;
            default: cout << "Invalid choice!\n";
        }
    }
}
