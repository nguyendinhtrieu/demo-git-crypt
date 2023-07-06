# Demo git-crypt

## 1. What is `git-crypt`
- Git-crypt is an open-source extension for Git that provides transparent file-level encryption for Git repositories. It allows you to encrypt specific files or directories within a Git repository, ensuring that only authorized users with the encryption key can access and decrypt the protected files.

## 2. Setup
### 2.1 Setting up GPG
- The purpose of using GPG (GNU Privacy Guard) in Git-crypt is to provide secure encryption and decryption of files within a Git repository.
- If you are using ubuntu, you can install via `apt-get`:
  ```shell
  sudo apt-get install gnupg
  ```
- Then, you can generate GPG key
  ```shell
  gpg --full-generate-key
  ```
### 2.2 Setting up git-crypt cli
- If you are using ubuntu, you can install via `apt-get`:
    ```shell
    sudo apt-get install git-crypt
    ```

## 3. Setting git-crypt for project
- Clone the git project
- Init git-crypt for project
  ```shell
  git-crypt init
  ```
- Create `.gitattributes` configuration file (will be explained in [Section 4](#4-explain-project-and-files))
- Add GPG user for project
  ```shell
  git-crypt add-gpg-user {name}
  ```
## 4. Explain project and files
- `.git-crypt`: `git-crypt add-gpg-user` will add and commit a GPG-encrypted key file in the `.git-crypt` directory of the root of your repository.
- `not_secretdir`: This folder store files which are not encrypted.
- `secretdir`: This folder store files which are encrypted.
- `.gitattributes`: file is used to specify the files that should be encrypted using Git-crypt. The `.gitattributes` file is a text file that resides in the root directory of your Git repository.
- `my_key`: key to encrypt this project

## 5. Export shared key to decrypt files
```shell
git-crypt export-key {path/to/my_key}
```

## 6. After clone the project, you can decrypt files using shared key
```shell
git-crypt unlock {path/to/my_key}
```
- Now, everything you commit that is configured in `.gitattributes` will be encrypted when you push to the Github. 

## 7. Reference
- https://github.com/AGWA/git-crypt