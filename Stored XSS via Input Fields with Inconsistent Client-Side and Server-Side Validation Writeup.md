# Stored XSS via Account Creation Input Fields

## **Summary**

Two fields in the account creation form are vulnerable to Stored XSS in Openkm Community Edition Version: 6.3.12

1. The Name field accepts XSS scripts directly
2. The email field doesn't accept XSS scripts directly but tools like Burp Suite can be used to intercept POST requests and modify the value for the field

## **Production Information**
- **Project**: OpenKm
- **Version**: 6.3.1.2
- **Environment**: Docker Image openkm-ce:6.3.12

## **Steps to Reproduce**

### **Vector 1: Name Field**
1. Login with admin credentials
2. Click on Administration
3. Click on Users
	- http://localhost:8080/OpenKM/admin/Auth
 4. Create a new user and set `<script>alert('XSS')</script>` as the value for the Name field
	 - http://localhost:8080/OpenKM/admin/Auth?action=userCreate
 5. This will generate an alert box with the text "XSS"

<img width="573" height="243" alt="image" src="https://github.com/user-attachments/assets/0f0c02da-8cda-4ae1-9700-beb73723992b" />
<img width="553" height="184" alt="image" src="https://github.com/user-attachments/assets/f4871bff-77e7-4061-8aac-4b0871469735" />

### **Vector 2: Email Field**
1. Use a tool like Burp Suite to intercept a POST request when creating a user
2. Replace the value of the `usr_email` field with `%3Cscript%3Ealert%28%27XSS%27%29%3C%2Fscript%3E`
<img width="774" height="440" alt="image" src="https://github.com/user-attachments/assets/9b3fe357-49d6-47e0-909b-4b681bb025d9" />
<img width="553" height="184" alt="image" src="https://github.com/user-attachments/assets/f4871bff-77e7-4061-8aac-4b0871469735" />




