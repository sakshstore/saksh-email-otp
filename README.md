  

saksh email otp
=======================

The OTP Verification Module is a tool that helps make your application more secure by using One-Time Passwords (OTPs). These are temporary codes sent to users to verify their identity. The module can generate these codes, send them via email, and check if the codes entered by users are correct. It uses Node.js and MongoDB, making it reliable and scalable for different applications.

One of the best features of this module is that it allows you to use your own email sending service. You can provide a custom function to send OTPs, which means you can use any email provider or SMTP server you prefer. This flexibility ensures that the OTPs are sent out exactly how you want them to be. The module also checks if the email addresses are valid before sending the OTPs, which helps in reducing errors.

The module also tracks user information like IP addresses and device details. This information is used to calculate a "confidence score," which helps determine how likely it is that the OTP request is legitimate. For example, if the IP address and device match the user's previous records, the confidence score will be higher. This score can range from 0 to 100, with higher scores indicating a higher likelihood that the request is genuine. This added layer of security helps protect against unauthorized access.

In summary, the OTP Verification Module is a versatile and powerful tool for adding OTP-based security to your application. It is easy to integrate, allows for custom email sending, and includes advanced security features like confidence scoring. Whether you're building a new app or enhancing an existing one, this module provides the tools you need to ensure secure and reliable user verification.

Installation
------------
 
    npm install saksh-email-otp

Initialization
--------------

### Initialize Database

To initialize the MongoDB connection, use the `sakshInitializeDB` function:

    const { sakshInitializeDB } = require('saksh-email-otp');
    
    sakshInitializeDB('mongodb://localhost:27017/yourdbname')
    .then(() => console.log('Database connected'))
    .catch(err => console.error('Database connection error:', err));

Usage
-----

### Send OTP

To send an OTP, use the `sakshHandleSendOTP` function. You can provide a custom email sending callback function:


```
    const { sakshHandleSendOTP } = require('saksh-email-otp');
    
    // Custom email sending callback function
    const sendEmailCallback = async (email, otp) => {
    const mailer = require('saksh-mailer');
    
    // Example SMTP configuration
    const smtpConfig = {
    host: 'smtp.example.com',
    port: 587,
    secure: false, // true for 465, false for other ports
    auth: {
    user: 'user@example.com',
    pass: 'userpassword',
    },
    };
    
    const transporter = mailer.createTransport(smtpConfig);
    
    const mailOptions = {
    from: smtpConfig.auth.user,
    to: email,
    subject: 'Your OTP Code',
    text: `Your OTP is: ${otp}`,
    };
    
    const info = await transporter.sendMail(mailOptions);
    console.log('Email sent:', info.response);
    };
    
    // Send OTP
   

   

var deviceInfo = {
    userAgent: 'Mozilla/5.0',
    platform: 'Win32',
    screenResolution: '1920x1080',
    browser: 'Chrome'
};


var ip = '192.168.1.1';

var email = 'user@example.com';




   sakshHandleSendOTP(email, ip, deviceInfo, sendEmailCallback).then(result => {


    console.log(result);
});

```


### Validate OTP

```
To validate an OTP, use the `sakshHandleValidateOTP` function:

    const { sakshHandleValidateOTP } = require('saksh-email-otp');

    // Validate OTP
sakshHandleValidateOTP(email, '762636', ip, deviceInfo).then(result => {
    console.log(result);
});

```


Functions
---------

### `sakshInitializeDB(uri)`

Initializes the MongoDB connection.

*   `uri` (string): The MongoDB connection URI.

### `sakshHandleSendOTP(email, ip, deviceInfo, sendEmailCallback)`

Sends an OTP to the specified email address.

*   `email` (string): The recipient's email address.
*   `ip` (string): The user's IP address.
*   `deviceInfo` (object): The user's device information.
*   `sendEmailCallback` (function): The callback function to send the email.

### `sakshHandleValidateOTP(email, otp, ip, deviceInfo)`

Validates the submitted OTP.

*   `email` (string): The user's email address.
*   `otp` (string): The OTP submitted by the user.
*   `ip` (string): The user's IP address.
*   `deviceInfo` (object): The user's device information.

Internal Functions
------------------

### `sakshGenerateOTP()`

Generates a One-Time Password (OTP).

### `sakshSendOTPEmail(email, otp, sendEmailCallback)`

Sends an OTP via email using a callback function.

### `sakshIsValidEmail(email)`

Validates if the provided email address is in a correct format.

### `sakshStoreOTP(email, otp, ip, deviceInfo)`

Stores the generated OTP along with additional metadata.

### `sakshCalculateConfidence(email, currentIP, currentDeviceInfo)`

Calculates the confidence level of the user's identity based on the provided email, IP address, and device information.

### `sakshCalculateDistance([lat1, lon1], [lat2, lon2])`

Calculates the distance between two geographical coordinates using the Haversine formula.

### `sakshValidateOTP(email, submittedOTP, currentIP, currentDeviceInfo)`

Validates the submitted OTP for a given email address, IP address, and device information.

License
-------

This project is licensed under the MIT License. 


Support
-------

Susheel2339 at gmail.com
