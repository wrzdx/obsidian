Database security is the set of methods, policies, and technologies used to protect databases from unauthorized access, misuse, data loss, and attacks.

- Legal and ethical issues regarding the right to access certain information
  *Some information may be deemed to be private and cannot be accessed legally by unauthorized organizations or persons*
- Policy issues at the governmental, institutional, or corporate level
  *What kinds of information should not be made publicly available—for example, credit ratings and personal medical records*
- System-related issues such as the system levels
  *Whether a security function should be handled at the physical hardware level, the operating system level, or the DBMS level*
- The need in some organizations to identify multiple security levels
  *The security policy of the organization with respect to permitting access to various classifications of data must be enforced*

## Threats to Databases
Threats to databases can result in the loss or degradation of some or all of the following commonly accepted security goals: integrity, availability, and confidentiality.

- **Loss of integrity** – Database integrity refers to the requirement that information be protected from improper modification.
- **Loss of availability** – Database availability refers to making objects available to a human user or a program who/which has a legitimate right to those data objects
- **Loss of confidentiality** – Database confidentiality refers to the protection of data from unauthorized disclosure

## Control Measures
Four main control measures are used to provide security of data in databases:
- **Access control** – Access control decides who is allowed to access which data and what actions they can perform.
- **Inference control** – Inference control prevents users from figuring out sensitive information indirectly.
- **Flow control** – Flow control prevents information from flowing from a higher security level to a lower security level.
- **Data encryption** – Encryption transforms data into an unreadable form so that unauthorized people cannot understand it.

## Database Attacks
- **Unauthorized privilege escalation** – This attack is characterized by an individual attempting to elevate his or her privilege by attacking vulnerable points in the database systems.
- **Privilege abuse** – An administrator who is allowed to change student information can use this privilege to update student grades without the instructor’s permission.
- **Denial of service (DOS) attack** – It is a general attack category in which access to network applications or data is denied to intended users by overflowing the buffer or consuming resources.
- **Weak authentication** – If the user authentication scheme is weak, an attacker can impersonate the identity of a legitimate user by obtaining her login credentials.

## SQL Injection
In an SQL injection attack, the attacker injects a string input through the application, which changes or manipulates the SQL statement to the attacker’s advantage.

An SQL injection attack can harm the database in various ways, such as unauthorized manipulation of the database or retrieval of sensitive data.

>[!abstract] 
>Main idea: Instead of entering normal input, the attacker enters SQL code.


### Preventing SQL Injection
**Key defences:**
- *Prepared statements* – Use parameterized queries so input is never interpreted as SQL code.
- *Input validation* – Check type, length, and format; prefer allow-lists for accepted values.
- *Least privilege* – Run the application with minimal database rights and avoid admin accounts.
- *Error handling & testing* – Hide detailed DB errors and test regularly for injection weaknesses.

