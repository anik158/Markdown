# DocTime Sign Up/Log In Process Documentation for Patients

The registration process on `DocTime` is designed to be user-friendly and secure, utilizing a One-Time Password (OTP) system. This document outlines the process in detail.

## OTP Sign Up

The registration process begins with the user signing up via OTP. The user must provide their phone number, after which an OTP is dispatched to the given number.

## Web Application Sign Up

On the web application, users can browse through the `DocTime` site and see what `DocTime` offers to their users. There are several ways for users to sign up:

1. **Doctor Consultation**: If a user browses through the doctor lists and wants to have a consultation with a doctor but has not signed up or registered, the user can pick a doctor of their interest and then click the option `Book Online Appointment` or `See Doctor Now`. A form will appear asking for the phone number with the country code. If the user clicks on `Send OTP`, a POST method API is invoked, `https://apidev.doctime.com.bd/api/authenticate`.

2. **Health Care and Protect Plans**: Another approach for registration or sign up is through `DocTime Health Care and Protect Plans`. If the user chooses a plan and clicks on `Subscribe now`, the user will be prompted with a pop-up which has the plans packages. After that, if the user clicks on `Subscribe Now` on the pop-up, the user will be given a form for the country code and a phone number for OTP.

3. **Direct Login**: Another way is to directly go to the `Login` button on the homepage and from there, provide the phone number for OTP.

Though there are different ways to sign up or registration, the same API will be called which is described in `Snippet 1` and `Snippet 2`.

## Mobile Application Sign Up

For the mobile application, the registration process is more streamlined. Users are not able to browse the `DocTime` application without signing up or registering. Upon opening the mobile application, users are asked to sign up or register through OTP, a process known as `Simple Login`.

If the user provides the correct credentials, all the APIs mentioned in the *API Details 1* section will be invoked. This completes the registration process on the `DocTime` mobile application. It’s designed to be user-friendly and secure, ensuring a smooth user experience.

## API Details 1

### Snippet 1 (OTP Request)

`https://apidev.doctime.com.bd/api/authenticate` this API allows the patient to request an OTP for login or registration.

```
Description:
    1. Patient can request OTP for login
    2. Patient can also request for registration

Body params:
    1. country_calling_code: Country calling code
    2. contact_no: Any valid contact no except country code. Ex 01700000000
```

JSON

```json
{
    "country_calling_code": "88",
    "contact_no": "01611717505",
    "timestamp": "1681794612"
}
```

### Snippet 2 (OTP Validation)

If the user enters the correct OTP and clicks ‘Confirm Code’, the `https://apidev.doctime.com.bd/api/authenticate/otp/verify` API is called. This API is for validating the OTP. After successful validation, an existing user will be logged in and a new user will be registered as a new patient.

```
Description:
    1. This API is for validate OTP
    2. After successfully validate existing user will be 
   logged in and the new user will be registered as a new patient.

Body params:
    1. country_calling_code: Country calling code
    2. contact_no: Any valid contact no except country code. Ex 01700000000
    3. otp: Provide OTP.
```

JSON

```json
{
    "country_calling_code": "88",
    "contact_no": "01611717505",
    "otp": "123456"
}
```

Upon successful verification, the system redirects the user to the `DocTime` dashboard/homepage via the `https://admindev.doctime.com.bd/api/users/profile` endpoint.

Following successful sign-up, the user has the option to add a password and email to their profile. This completes the registration process on `DocTime`.

## DocTime Login Procedure for Patients

The login procedure on `DocTime` has been designed to be user-friendly and secure. Users can log in with an OTP without needing to enter a password each time. The back-end works as explained in the *API Details 1* section.

However, if a user wants to add their email and password, they can do so. They need to go to their profile and add an email and password. After that, the user will have to go to the login page where the phone number is asked for OTP. They can choose the option `or, login using a password` in both the mobile application and web application. if the user choses the email/phone or password option API Details 3 api will be invoked.

## API Details 2

### Snippet 3 (Login Request)

The `https://admindev.doctime.com.bd/api/login` API allows the patient to request for login using email and password.

```
Body params:

1. contact: Email / Contact No
    - Email: any valid email can be acceptable
    - Contact_no: any valid contact no except country code. Ex 01700000000
2. password: your account password
```

JSON

```json
{
    "contact": "patient1@example.com",
    "password": "secret"
}
```

Upon successful validation, the system redirects the user to the `DocTime` dashboard/homepage via the `https://admindev.doctime.com.bd/api/users/profile` endpoint. This completes the login process on `DocTime`. 
