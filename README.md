### AppDoot Api Setup and Deployment

**Problem Statement:**
AppDoot is a platform where an admin can add Android apps and assign points for users to earn by downloading these apps. The user-facing side allows users to view the apps, track their points, and upload screenshots to confirm app downloads.

Deployment Link:
https://dheeraj19.pythonanywhere.com/api/v1/user/

Video Link:https://drive.google.com/file/d/1CTrbLM8DVOKdYtmUklLjGNMYHG2Mindd/view?usp=sharing

**API Endpoints:**

1. **User Authentication:**
   - **Register a new user:**
     - **Endpoint:** `/api/v1/user/`
     - **Method:** `POST`
     - **Request Body:**
       ```json
       {
         "username": "user1",
         "email": "user1@example.com",
         "password": "yourpassword"
       }
       ```

   - **Login:**
     - **Endpoint:** `/api/v1/user/login/`
     - **Method:** `POST`
     - **Request Body:**
       ```json
       {
         "username": "user1",
         "password": "yourpassword"
       }
       ```

2. **App Management (Admin Facing):**
   - **Upload a new app:**
     - **Endpoint:** `/api/v1/android/apps_view/upload_app/`
     - **Method:** `POST`
     - **Request Body:**
       ```json
       {
         "name": "App Name",
         "description": "App Description",
         "points": 100
       }
       ```

3. **User Tasks (User Facing):**
   - **Retrieve user tasks and available apps:**
     - **Endpoint:** `/api/v1/android/apps_view/user_tasks/`
     - **Method:** `GET`

   - **Upload a screenshot for a task:**
     - **Endpoint:** `/api/v1/android/apps_view/upload_screenshot/`
     - **Method:** `POST`
     - **Request Body:**
       ```json
       {
         "app_id": 1,
         "screenshot": "screenshot_file.png"
       }
       ```

**Project Setup:**

1. **Clone the Repository:**
   ```bash
   git clone https://github.com/DheerajDubey19/AppDoot.git
   cd AppDoot
   ```

2. **Create a Virtual Environment:**
   ```bash
   python3 -m venv venv
   source venv/bin/activate   # On Windows: venv\Scripts\activate
   ```

3. **Install Dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

4. **Configure Environment Variables:**
   - Create a `.env` file in the project root:
     ```bash
     touch .env
     ```
   - Add your environment variables, such as `SECRET_KEY`, `DEBUG`, `DATABASE_URL`, etc.

5. **Run Database Migrations:**
   ```bash
   python manage.py makemigrations
   python manage.py migrate
   ```

6. **Create a Superuser (Optional for Admin Access):**
   ```bash
   python manage.py createsuperuser
   ```

7. **Collect Static Files:**
   ```bash
   python manage.py collectstatic
   ```

8. **Run the Development Server:**
   ```bash
   python manage.py runserver
   ```

**Deployment on PythonAnywhere:**

1. **Clone Your Git Repository:**
   - Open a Bash console in PythonAnywhere.
   - Clone your repository:
     ```bash
     git clone https://github.com/dheeraj19/AppDoot.git
     ```

2. **Set Up a Virtual Environment:**
   - Create and activate a virtual environment:
     ```bash
     mkvirtualenv --python=/usr/bin/python3.10 appdootenv
     workon appdootenv
     ```
   - Install dependencies:
     ```bash
     pip install -r /home/dheeraj19/AppDoot/requirements.txt
     ```

3. **Configure Django Settings:**
   - Update `settings.py` with your PythonAnywhere domain and configure static and media files.

4. **Set Up the Web App:**
   - Go to the "Web" tab on PythonAnywhere.
   - Add a new web app with manual configuration and set paths for the source code and virtual environment.
   - Set the source code path to /home/dheeraj19/AppDoot/.
   - Set the virtual environment path to /home/dheeraj19/.virtualenvs/appdootenv.
   - Configure the WSGI file:
    - Open the WSGI file from the "Web" tab.
    - Edit it to point to your Django project:
       
       import os
       import sys

       path = '/home/dheeraj19/AppDoot'
       if path not in sys.path:
           sys.path.append(path)

       os.environ['DJANGO_SETTINGS_MODULE'] = 'AppDoot.settings'

       from django.core.wsgi import get_wsgi_application
       application = get_wsgi_application()
   

5. **Run Migrations and Collect Static Files:**
   - Run the following commands:
     ```bash
     python manage.py migrate
     python manage.py collectstatic
     ```

6. **Reload the Web App:**
   - Reload the app from the "Web" tab on PythonAnywhere.

This will successfully deploy the AppDoot project on PythonAnywhere using your username `dheeraj19`.

