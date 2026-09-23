# Week 3 – Cracking a Password Protected PDF (John the Ripper + Networkwalks Tools)

## What this lab was about

During Week 3 of my Networkwalks Cybersecurity training, I worked on recovering passwords from protected PDF files by extracting their crackable hashes and performing dictionary-based attacks.

I completed the practical using two separate approaches. The first method involved **John the Ripper** through its **Johnny GUI**, while the second method used **Networkwalks' browser-based Hash Calculator and Password Cracker**.

Both methods successfully recovered the passwords and were verified by using the recovered passwords to open the protected PDF files. Since the tools and workflow were different, both approaches are documented separately below.

This practical was performed entirely in an authorized cybersecurity training environment using sample files provided for the exercise. These techniques should only be used on files, accounts, or systems where you have explicit permission to perform testing.

---

## Goals for the exercise

- Understand how password hashes are associated with encrypted PDF files and why the original password cannot simply be read from the file.
- Extract a PDF password hash using two different tools.
- Perform a practical dictionary attack against the extracted hash.
- Verify that the recovered password can actually unlock the protected PDF.
- Learn how to use the **Johnny GUI** with John the Ripper.
- Document the complete password-recovery workflow for future reference and authorized cybersecurity practice.

---

## Kit used

| Tool | What I used it for |
|---|---|
| OnlineHashCrack – PDF Hash Extractor | Extracting a pdf2john-compatible hash from the protected PDF |
| Johnny (GUI for John the Ripper) | Loading the extracted hash and performing the dictionary attack |
| John the Ripper 1.9.0-jumbo-1 | Password-cracking engine used by Johnny |
| Networkwalks Hash Calculator | Extracting the PDF hash through a browser-based tool |
| Networkwalks Password Cracker | Performing a dictionary attack directly through the browser |
| Notepad / Text Editor | Saving the extracted hash before importing it into Johnny |
| Adobe Acrobat Reader | Testing and opening the recovered PDF files |

---

## Route 1: John the Ripper via Johnny

### Step 1 – Pulling the hash out of the PDF

The password of an encrypted PDF is not stored in a directly readable format. Before a cracking tool can test possible passwords, information from the protected PDF must first be converted into a compatible hash format.

For this step, I used the **PDF Hash Extractor** tool. I uploaded the protected PDF, and the tool processed it using `pdf2john` to generate a PDF hash beginning with:

`$pdf$4*4*128*-1060*1*16*...`

![PDF file uploaded to hash extractor](hash_file_uploaded.png)

After processing was completed, the tool displayed the generated hash in a text field.

![Generated hash value](hash_value_of_file.png)

![Hash value shown in full](hash_value(a).png)

### Step 2 – Getting the hash somewhere Johnny could read it

Johnny requires the extracted hash to be provided through a file. I copied the generated hash into a text file, saved it as `hash1.txt`, and placed the file inside the working directory.

![Hash saved into a text file](load_the_hash_text.png)

### Step 3 – Pointing Johnny at the John the Ripper executable

Before launching the attack, Johnny needs to know the location of the John the Ripper executable.

I opened the Settings section and configured the path to the downloaded John the Ripper jumbo version. Johnny then successfully detected:

`John the Ripper 1.9.0-jumbo-1`

![Setting the John the Ripper executable path inside Johnny](loading_JTR_exe.png)

### Step 4 – Loading the hash and starting the attack

After configuring Johnny, I opened the saved hash file using the **Open password file** option.

Once the hash was loaded correctly, I started a new attack session.

![Loading the saved hash file and starting the attack in Johnny](load.png)

### Step 5 – Result

Johnny successfully completed the dictionary attack and identified the password as:

**password1**

![Johnny reporting the password has been cracked](fond_password.png)

### Step 6 – Confirming the recovered password

Finding a password inside the cracking tool is only part of the verification process. I opened the protected PDF and entered the recovered password.

The document unlocked successfully, confirming that the recovered password was correct.

![Applying the recovered password to unlock the PDF](apply_password_for_unlock.png)

![PDF opened successfully after unlocking](opend_pdf.png)

### Additional Johnny tests

I repeated the same workflow with two additional sample PDF hashes to confirm that the process worked consistently.

#### pdf2

![Finding hash value of pdf2](pdf2_hash_value.png)

![Hash value of pdf2 in txt file](pdf2_hash_value_in_text_file.png)

![Opening a second hash inside Johnny](open_hash2_in_johnny.png)

![Attack completing and password recovered](perform_attack_fond_password.png)

![After finding password entered in pdf for confirmation](pdf2_password_entered.png)

![Opened Pdf2](opened_pdf2.png)

#### pdf3

![Finding hash value of pdf3](pdf3_hash_value.png)

![Hash value of pdf3 in txt file](pdf3_hash_value_in_text_file.png)

![Opening a third hash inside Johnny](open_hash3_in_johnny.png)

![Attack completing and password recovered for the third file](perfom_attack_and_fond_password_pdf3.png)

![After finding password entered in pdf for confirmation](pdf3_password_entered.png)

![Opened Pdf3](opened_pdf3.png)

---

## Route 2: Networkwalks' own browser based tools

To compare the locally installed approach with a browser-based workflow, I performed the same exercise using **Networkwalks' own training tools**.

This approach follows the same basic sequence: first extract the PDF hash and then perform a dictionary attack. However, the process is handled through the browser instead of requiring a local installation of John the Ripper.

For this method, I used fresh copies of the sample PDFs downloaded from the training environment.

### Step 1 – Extracting the hash with the Hash Calculator

The Networkwalks Hash Calculator provides a dedicated PDF option. It processes the selected PDF and generates a `$pdf$` style hash similar to the output produced by `pdf2john`.

![Hash Calculator tool homepage](hash_calculator.png)

![Online hash tool interface](online-hash.png)

I uploaded the first sample PDF. The tool identified the file as encrypted and generated the corresponding hash together with information such as the revision, version, and key length.

![Uploading PDF1 into the Hash Calculator](upload_pdf1_in_calculator.png)

![PDF1 hash value generated by the Hash Calculator](hash_value_pdf1_via_hash_calculator.png)

### Step 2 – Feeding the hash into the Password Cracker

The Password Cracker works using the same basic dictionary-attack concept used by John the Ripper.

It tests candidate passwords from a wordlist, generates their hashes, and compares them with the target hash until a matching value is found.

I copied the hash generated by the Hash Calculator and entered it into the Password Cracker.

![Password Cracker tool interface](password_craker.png)

![Pasting the extracted hash into the Password Cracker](paste_hash_value.png)

### Step 3 – Watching the attack run

After starting the attack, the tool processed the available wordlist and tested candidate passwords against the extracted hash.

The process continued until a matching password was identified.

![PDF1 password found by the cracker](fond._pdf1_password.png)

![Confirmation of the recovered PDF1 password](confirmation_pdf1_password.png)

### Step 4 – Unlocking the file

After the password was recovered, I entered it into the protected PDF to verify the result.

The PDF opened successfully, confirming that the recovered password was valid.

![PDF1 opened successfully with the recovered password](opened_pdf1.png)

### Repeating the process for PDF2 and PDF3

To verify that the workflow was repeatable, I performed the same extraction and password-recovery process on two additional sample PDFs.

### PDF2

![Uploading PDF2 to the Hash Calculator](upload_psf2_in_hash_calculator.png)

![PDF2 hash value extracted](pdf2_hash_value.png)

![PDF2 password found](pdf2_password_fond.png)

![PDF2 password confirmed](confirmation_pdf2.png)

![PDF2 opened](opened_pdf2(2).png)

### PDF3

![Uploading PDF3 to the Hash Calculator](upload_pdf3_in_hash_calculator.png)

![PDF3 hash value found](fond_pdf3_hash_value.png)

![PDF3 password cracked successfully](cracked_pdf3_password.png)

![PDF3 password entered](put_pdf3_password.png)

![PDF3 opened, alternate view](opened_pdf3(2).png)

---

## What I learned from the exercise

Performing the same practical using both an offline application and a browser-based tool helped me understand several important concepts more clearly.

- A hash is not simply the password stored in a scrambled form. It is a one-way representation, so dictionary attacks work by generating hashes from possible passwords and comparing them against the target hash.
- The passwords in these sample files were recovered quickly because they were simple and common values that are likely to appear near the beginning of password dictionaries.
- Hash extraction is an important part of the process. If the extracted hash is incomplete or contains incorrect formatting, salt, or revision information, the cracking tool will not be able to work correctly.
- The underlying password-cracking process remains similar even when different interfaces are used. Johnny requires configuration of the John the Ripper executable and attack session, while the browser-based tool handles much of that configuration automatically.
- Verifying the recovered password by actually opening the protected PDF provides an additional confirmation that the result is genuine.

---

## Why this matters from a defensive angle

This practical showed how quickly weak passwords can potentially be recovered when they are included in commonly available password dictionaries.

The exercise demonstrates why short, predictable, and commonly used passwords provide limited protection when an attacker obtains the corresponding hash.

Important defensive lessons include:

- Avoid passwords that are commonly found in password dictionaries. **password1** is a simple example of a weak and predictable password.
- Use longer and less predictable passwords rather than depending only on complexity requirements such as uppercase letters, numbers, or special characters.
- Enable multi-factor authentication where it is available so that a compromised password does not automatically provide complete access.
- Organizations handling sensitive documents should avoid relying solely on PDF password protection as their only security control.

---

## Training details

- **Program:** Networkwalks Cybersecurity & Ethical Hacking Training
- **Week:** 3
- **Modules:** Project Module 1 (Password Cracking with JTR) & Project Module 2 (Password Cracking with Networkwalks Tools)
- **Task:** Password recovery from an encrypted PDF using John the Ripper / Johnny and Networkwalks' Hash Calculator / Password Cracker
- **Focus area:** Applied cybersecurity / ethical hacking fundamentals

---

## A note on ethics

All activities documented in this repository were performed using sample files specifically provided for the training exercise within an authorized laboratory environment.

Password-cracking techniques should only be used against systems, files, or accounts that you own or have explicit permission to test.

Using these techniques against unauthorized targets may be illegal. This repository is intended for educational purposes and authorized cybersecurity training only.

---

## 👤 Author

**Muhammad Ahsan**

Cybersecurity Trainee | NetworkWalks Academy

🔗 LinkedIn: [[Muhammad Ahsan](https://www.linkedin.com/in/mahsan-mushtaq/)]

**Project Information:** Program: Cybersecurity & Ethical Hacking at NetworkWalks | Week: 03
