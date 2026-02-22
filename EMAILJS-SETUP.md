# EmailJS Setup for Student Registration Dashboard

This README explains how to configure EmailJS to send automated confirmation emails and which values to replace in the code.

**Steps to create and configure an EmailJS account**

1. Sign up at https://www.emailjs.com and log in.
2. Add an email service: go to **Email Services** and connect your provider (Gmail, SMTP, etc.). Note the **Service ID** (e.g. `service_xxxxxxx`).
3. Create an email template: go to **Email Templates** → **Create new template**. Add template variables you will use (example: `to_email`, `name`, `rollno`, `branch`, `year`). Save and note the **Template ID** (e.g. `template_xxxxxxx`).
4. Get your Public Key (User ID): open **Integration** (or Account settings) and copy the **Public Key** (sometimes called `userID` or `publicKey`).
5. Test the template within EmailJS by using the built-in Send Test feature to ensure emails are delivered.

**What to include in your web page**

- Include the EmailJS SDK (example used in this project):

  <script src="https://cdn.jsdelivr.net/npm/@emailjs/browser@4/dist/email.min.js"></script>

- Initialize EmailJS with your Public Key in JavaScript:

  `emailjs.init({ publicKey: "YOUR_PUBLIC_KEY" });`

- Send an email using the Service ID and Template ID:

  `emailjs.send("YOUR_SERVICE_ID", "YOUR_TEMPLATE_ID", { /* template params */ })`

**Exactly what to replace in this project**

- Open [index.html](index.html) and update the following:
  - Replace the public key in the `emailjs.init(...)` call with your Public Key.
  - Replace the first argument of `emailjs.send(...)` with your Service ID.
  - Replace the second argument of `emailjs.send(...)` with your Template ID.
  - Make sure the template parameter object keys match the variable names used in your EmailJS template (for example: `to_email`, `name`, `rollno`, `branch`, `year`).

Example replacements in the current code:

- `emailjs.init({ publicKey: "_xxxxxxxxxxxxxxxx" });` → `emailjs.init({ publicKey: "YOUR_PUBLIC_KEY" });`
- `emailjs.send("service_xxxxxxx", "template_xxxxxxx", { to_email: email, name, rollno, branch, year })`
  → `emailjs.send("YOUR_SERVICE_ID", "YOUR_TEMPLATE_ID", { to_email: email, name, rollno, branch, year })`

**Security & best practices**

- Do NOT commit real keys or service/template IDs to a public repository. Treat the Public Key as sensitive in public projects.
- For production, consider sending emails server-side (to keep secrets private) or use environment variables and a build step that injects keys securely.

**Troubleshooting**

- If emails fail, check the browser console for errors and verify the Service ID, Template ID and Public Key.
- Verify your EmailJS service is active and that the template variables match exactly.
- Use the EmailJS dashboard's test/send feature to validate templates.
