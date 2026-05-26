# intentionally_vulnerable_demo.py
#
# This file contains several COMMON and INTENTIONAL security vulnerabilities
# for educational/testing purposes only.
# Do NOT deploy this in a real environment.

import os
import sqlite3
import pickle

DB_NAME = "users.db"


def setup_database():
    conn = sqlite3.connect(DB_NAME)
    cur = conn.cursor()

    cur.execute(
        "CREATE TABLE IF NOT EXISTS users (username TEXT, password TEXT)"
    )

    cur.execute(
        "INSERT INTO users VALUES ('admin', 'supersecret')"
    )

    conn.commit()
    conn.close()


# --------------------------------------------------
# Vulnerability #1: SQL Injection
# --------------------------------------------------
def vulnerable_login(username, password):
    conn = sqlite3.connect(DB_NAME)
    cur = conn.cursor()

    # Unsafe string concatenation
    query = (
        "SELECT * FROM users WHERE username = '"
        + username
        + "' AND password = '"
        + password
        + "'"
    )

    print(f"[DEBUG] Executing query: {query}")

    cur.execute(query)
    result = cur.fetchone()

    conn.close()

    if result:
        print("Login successful!")
    else:
        print("Invalid credentials.")


# --------------------------------------------------
# Vulnerability #2: Command Injection
# --------------------------------------------------
def ping_host(host):
    # Dangerous use of os.system with user input
    command = f"ping -c 1 {host}"

    print(f"[DEBUG] Running command: {command}")

    os.system(command)


# --------------------------------------------------
# Vulnerability #3: Insecure Deserialization
# --------------------------------------------------
def load_user_data(filename):
    # Unsafe pickle loading
    with open(filename, "rb") as file:
        data = pickle.load(file)

    print("Loaded object:", data)


# --------------------------------------------------
# Vulnerability #4: Hardcoded Secret
# --------------------------------------------------
API_KEY = "MY_SUPER_SECRET_API_KEY_12345"


# --------------------------------------------------
# Vulnerability #5: Path Traversal
# --------------------------------------------------
def read_file(filename):
    # No sanitization of user-controlled path
    with open(filename, "r") as file:
        contents = file.read()

    print(contents)


# --------------------------------------------------
# Main Menu
# --------------------------------------------------
def main():
    setup_database()

    while True:
        print("\n=== Vulnerable Demo App ===")
        print("1. Login")
        print("2. Ping Host")
        print("3. Load Pickle File")
        print("4. Read File")
        print("5. Exit")

        choice = input("Choose an option: ")

        if choice == "1":
            username = input("Username: ")
            password = input("Password: ")
            vulnerable_login(username, password)

        elif choice == "2":
            host = input("Host to ping: ")
            ping_host(host)

        elif choice == "3":
            filename = input("Pickle filename: ")
            load_user_data(filename)

        elif choice == "4":
            filename = input("File to read: ")
            read_file(filename)

        elif choice == "5":
            break

        else:
            print("Invalid option.")


if __name__ == "__main__":
    main()
