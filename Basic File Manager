#include <iostream>
#include <filesystem>
#include <fstream>

using namespace std;
namespace fs = std::filesystem;

void listFiles(const fs::path& directory) {
    cout << "Files in directory: " << directory << endl;
    for (const auto& entry : fs::directory_iterator(directory)) {
        cout << entry.path().filename().string() << endl;
    }
}

void createDirectory(const fs::path& directory) {
    if (fs::create_directory(directory)) {
        cout << "Directory created: " << directory << endl;
    } else {
        cout << "Failed to create directory or it already exists." << endl;
    }
}

void copyFile(const fs::path& source, const fs::path& destination) {
    try {
        fs::copy(source, destination);
        cout << "Copied: " << source << " to " << destination << endl;
    } catch (const fs::filesystem_error& e) {
        cout << "Error copying file: " << e.what() << endl;
    }
}

void moveFile(const fs::path& source, const fs::path& destination) {
    try {
        fs::rename(source, destination);
        cout << "Moved: " << source << " to " << destination << endl;
    } catch (const fs::filesystem_error& e) {
        cout << "Error moving file: " << e.what() << endl;
    }
}

int main() {
    string command;
    fs::path currentPath = fs::current_path();

    while (true) {
        cout << "\nCurrent Directory: " << currentPath << "\n";
        cout << "Enter command (ls, cd, mkdir, cp, mv, exit): ";
        cin >> command;

        if (command == "ls") {
            listFiles(currentPath);
        } else if (command == "cd") {
            string dir;
            cin >> dir;
            fs::path newPath = currentPath / dir;
            if (fs::exists(newPath) && fs::is_directory(newPath)) {
                currentPath = newPath;
            } else {
                cout << "Directory does not exist." << endl;
            }
        } else if (command == "mkdir") {
            string dir;
            cin >> dir;
            createDirectory(currentPath / dir);
        } else if (command == "cp") {
            string source, dest;
            cin >> source >> dest;
            copyFile(currentPath / source, currentPath / dest);
        } else if (command == "mv") {
            string source, dest;
            cin >> source >> dest;
            moveFile(currentPath / source, currentPath / dest);
        } else if (command == "exit") {
            break;
        } else {
            cout << "Unknown command." << endl;
        }
    }

    return 0;
}
