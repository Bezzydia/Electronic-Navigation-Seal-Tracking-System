# Electronic-Navigation-Seal-Tracking-System
NaviSeal is a Telegram bot for real-time monitoring and management of electronic navigation seals with integrated geolocation tracking.
Key Features ✨
Real-time seal status monitoring (Active/Inactive)
Electronic Seal (ЭНП) activation/deactivation
Yandex Maps integration for location verification
Complete audit trail with timestamped status history
GRZ-based identification for quick seal lookup
Intuitive Telegram interface with inline keyboards

Technical Implementation 🧠

![image](https://github.com/user-attachments/assets/d9a5e6df-31f3-4a6e-a9f9-ac428f55de42)



Installation ⚙️
Clone repository:
bash
git clone https://github.com/yourusername/naviseal-tracker.git
cd naviseal-tracker
Install dependencies:
bash
pip install aiogram sqlite3 requests python-dotenv
Configure environment:
env
BOT_TOKEN=your_telegram_bot_token
Initialize seal database:
python
python init_db.py

Database Schema 📊
Diagram
Code

![image](https://github.com/user-attachments/assets/69ed0fc7-b6db-4714-8136-96ad1f5eb458)


Usage Examples 💬
Find Navigation Seal
text
User: /find
Bot: Выберите пломбу для просмотра:
[Inline Keyboard with GRZ options]
Update Seal Status
text
User: /status
Bot: Выберите пломбу для изменения статуса:
[GRZ Selection → Action Selection]
Status Change Confirmation
text
Bot: Статус пломбы А123ВС77 изменен: Активирована ✅
Core Functionality 🛠️
Seal Tracking
Real-time status monitoring
Location verification via coordinates
Route information display
Last update timestamp

Status Management
Electronic seal activation (Активировать ЭНП)
Electronic seal deactivation (Деактивировать ЭНП)
Complete audit history
Instant status updates


Commands Overview
Command	Description	State Management
/start	Initializes bot	Clears state
/find	Find navigation seal	FindSeal.choosing_grz
/status	Change seal status	StatusUpdate.choosing_grz


Setup Instructions 🚀
Create a Telegram bot via @BotFather

Configure database:

python
# Initialize seal database
cursor.execute('''
CREATE TABLE IF NOT EXISTS seals (
    grz TEXT PRIMARY KEY,
    status TEXT,
    route TEXT,
    latitude REAL,
    longitude REAL,
    last_update DATETIME
)
''')

cursor.execute('''
CREATE TABLE IF NOT EXISTS status_history (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    grz TEXT,
    status TEXT,
    timestamp DATETIME
)
''')
Add sample seals:

python
cursor.execute('''
INSERT INTO seals (grz, status, route, latitude, longitude, last_update)
VALUES 
    ('А123ВС77', 'Активирована ✅', 'Москва-Санкт-Петербург', 55.7558, 37.6173, CURRENT_TIMESTAMP),
    ('К456МН78', 'Деактивирована ❌', 'Казань-Уфа', 55.7961, 49.1064, CURRENT_TIMESTAMP)
''')
Security Features 🔒
GRZ-based authentication

Stateful session management

Audit trail for all status changes

Location verification

Timestamped operations
