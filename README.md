# Online Voting System (QKD Simulation)

**Repository:** Online-voting-system-using-Quantum-Key-Distribution

**Description:**  
This project is an **online voting platform** that integrates a **Quantum Key Distribution (QKD)**-inspired mechanism to secure votes.  
It ensures that votes are encrypted with randomly generated quantum-like keys before being stored.

---

## Features
- **Voter Module** – Cast votes securely using a QKD-based key generation.
- **Admin Module** – View decrypted results using stored QKD keys.
- **MySQL Database** – Stores voter, admin, and voting data.
- **Flask Backend** – Manages routes, authentication, and encryption logic.
- **Basic Frontend** – HTML templates for login, voting, and admin dashboard.

---

## Tech Stack
- **Backend:** Python (Flask)
- **Database:** MySQL (or MariaDB)
- **Frontend:** HTML, CSS
- **Other:** `mysql-connector-python` for DB connectivity

---

## ⚠ Security Notes
- The QKD implementation is **simulated**:
  - `generate_qkd_key()` returns a random bit-string.
  - Encryption is a simple XOR with that bit string.
  - This **does not** provide real quantum security.
- Current version:
  - Runs `debug=True` — disable in production.
  - Contains plaintext DB passwords in `app.py` — move to environment variables or a `.env` file.
  - Stores admin password in plaintext in SQL — use hashed passwords (bcrypt).
  - Includes `venv/` folder — remove from repository.

Do **not** deploy without proper security improvements.

---

## Project Structure

project-root/
├── app.py # Main Flask application
├── database/
│ └── voting_system.sql # Database schema + sample data
├── templates/ # HTML templates for different pages
│ ├── home.html
│ ├── admin_login.html
│ ├── admin_dashboard.html
│ ├── voting_ballot.html
│ └── voting_success.html
├── static/ # Static files (CSS, images)
│ ├── css/
│ │ └── style.css
│ └── images/
│ └── election.jpeg
└── venv/ # Virtual environment (should be .gitignored)

---

## Installation and Setup

1. **Clone the Repository**
    ```bash
    git clone https://github.com/Sivakeerthi-1211/Online-voting-system-using-Quantum-Key-Distribution.git
    cd Online-voting-system-using-Quantum-Key-Distribution
    ```

2. **Install Python (if not already installed)**  
   Download from [https://www.python.org/downloads/](https://www.python.org/downloads/)

3. **Create and Activate Virtual Environment** *(optional but recommended)*
    ```bash
    python -m venv venv
    venv\Scripts\activate   # For Windows
    source venv/bin/activate  # For Mac/Linux
    ```

4. **Install Dependencies**
    ```bash
    pip install Flask mysql-connector-python
    ```

5. **Set up the Database**
    - Make sure MySQL is running.
    - Import the SQL file:
      ```bash
      mysql -u root -p < database/voting_system.sql
      ```

6. **Configure `app.py`**
    - Edit database credentials:
      ```python
      app.config['MYSQL_HOST'] = 'localhost'
      app.config['MYSQL_USER'] = 'root'
      app.config['MYSQL_PASSWORD'] = ''
      app.config['MYSQL_DB'] = 'voting_system'
      ```
    - Set a secret key for Flask sessions:
      ```python
      app.secret_key = 'yoursecretkey'
      ```

7. **Run the App**
    ```bash
    python app.py
    ```
    Open [http://127.0.0.1:5000/](http://127.0.0.1:5000/) in your browser.

---

## Database Schema
The included `database/voting_system.sql` creates:
- `voters` table (`voter_id_number`, `name`)
- `votes` table (`voter_id_number`, `encrypted_vote`, `qkd_key`)
- `admin` table (`username`, `password`)

**Sample Data:**
- Voter IDs: `VOTER123`, `VOTER124`
- Admin: `admin` / `adminpassword`

---

## Recommended Improvements

- Remove `venv/` from repo and add `.gitignore`
- Use hashed passwords for admin
- Store secrets in environment variables
- Add proper validation & authentication
- Replace simulated QKD with a real quantum cryptographic library

---

## License

This project is licensed under the **MIT License** – see the LICENSE file for details.
