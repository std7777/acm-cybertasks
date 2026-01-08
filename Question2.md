# Q2: OSINT
flag obtained: ACM{1_kn0w_051n7}

## Write up

1. The description of the image held the challenge statement and the format of the flag.

   (Map it Out) | Your task is to use your Open Source INTelligence skills to find the flag hidden somewhere through out the internet | The trail of clues are laid        before you. Are your skills sharp enough to uncover them all and reach your goal. | Flag format: <ins>ACM{4ll_7h3_b357}</ins>

2. We check the metadata embeded in the image by exiftool (preinstalled in kali linux)

   <img width="901" height="421" alt="image" src="https://github.com/user-attachments/assets/9b3e30aa-6adb-4d7a-af7e-c8d59e7f1649" />

3. On investigating these clues we find a lead on X.com on the account @AncientDragon05.
   The profile contained further clues:
      link was present in the bio
      The term “vinegar”, hinting at a cipher
      The word “dracula”
      Removal of the letter “h”

   <img width="740" height="991" alt="image" src="https://github.com/user-attachments/assets/2ad4fe79-a621-44c5-9e7e-856ca7258d6b" />

4. The link in the bio leads to an account with a post with the title DTM{1_mg0g_051n7}. As informed above this isnt the format of the final flag. The above tweets indicate it needs to be encoded.

<img width="1207" height="790" alt="Screenshot 2026-01-08 235023" src="https://github.com/user-attachments/assets/3325534c-a6a8-466c-ae86-3c117642e510" />

5. The Vigenere cipher is the one required. We use the variant beaufort cipher, key as dracula and remove 'h' from the alphabets to get the final flag. ACM{1_kn0w_051n7}
   
   <img width="1902" height="872" alt="Screenshot 2026-01-08 235050" src="https://github.com/user-attachments/assets/b6e243a2-d8de-46b1-b626-c93d50c03ece" />
