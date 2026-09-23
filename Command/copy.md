# PowerShell File & Folder Commands

A quick reference for creating, copying, and deleting files and folders using PowerShell.

---

## 📁 Copy Files and Folders

### 1. Copy all files from one folder to another

```powershell
Copy-Item "C:\source\*" "C:\destination\" -Recurse
```

Example:

```powershell
Copy-Item "C:\Users\Anurag\Desktop\project1\*" "C:\Users\Anurag\Desktop\project2\" -Recurse
```

This copies the **contents** of `project1` into `project2`.

---

### 2. Copy the entire folder

```powershell
Copy-Item "C:\Users\Anurag\Desktop\project1" "C:\Users\Anurag\Desktop\project2" -Recurse
```

> `-Recurse` copies the folder and all files/subfolders inside it.

---

## 📄 Copy Content from One File to Another

### 3. Replace the content of an existing file

```powershell
Get-Content "source.txt" | Set-Content "destination.txt"
```

This copies all content from `source.txt` to `destination.txt`.

⚠️ **Important:** Existing content in `destination.txt` will be replaced.

---

### 4. Append content to an existing file

```powershell
Get-Content "source.txt" | Add-Content "destination.txt"
```

This adds the content of `source.txt` to the **end** of `destination.txt`.

Existing content will remain.

---

## 🗑️ Delete Files and Folders

### 5. Delete an empty folder

```powershell
Remove-Item "C:\Users\Anurag\Desktop\MyFolder"
```

---

### 6. Delete a folder and everything inside it

```powershell
Remove-Item "C:\Users\Anurag\Desktop\MyFolder" -Recurse
```

> `-Recurse` deletes the folder along with all files and subfolders.

---

### 7. Force delete a folder

```powershell
Remove-Item "C:\Users\Anurag\Desktop\MyFolder" -Recurse -Force
```

⚠️ **Warning:** This permanently deletes the folder and its contents. Use it carefully.

---

### 8. Delete a file inside an existing folder

```powershell
Remove-Item "C:\Users\Anurag\Desktop\MyFolder\test.txt"
```

If you are already inside the folder:

```powershell
Remove-Item "test.txt"
```

---

### 9. Delete multiple files

```powershell
Remove-Item "test.js", "server.js"
```

---

### 10. Delete all files with a specific extension

For example, delete all `.txt` files:

```powershell
Remove-Item "C:\Users\Anurag\Desktop\MyFolder\*.txt"
```

---

## 📂 Navigate Between Folders

### 11. See the current directory

```powershell
pwd
```

---

### 12. List files and folders

```powershell
ls
```

You can also use:

```powershell
Get-ChildItem
```

---

### 13. Go inside a folder

```powershell
cd myproject
```

Example:

```powershell
cd Desktop
```

---

### 14. Go back one folder

```powershell
cd ..
```

---

## 🆕 Create Files and Folders

### 15. Create a new file

```powershell
New-Item test.txt
```

---

### 16. Create a JavaScript file

```powershell
New-Item server.js
```

---

### 17. Create a folder

```powershell
New-Item -ItemType Directory myproject
```

Or simply:

```powershell
mkdir myproject
```

---

### 18. Create multiple files

```powershell
New-Item index.js, server.js, package.json
```

---

### 19. Create a file with content

```powershell
"Hello World" | Set-Content test.txt
```

---

## 💻 Open Project in VS Code

First, go to your project folder:

```powershell
cd Desktop\myproject
```

Then:

```powershell
code .
```

This opens the current folder in **VS Code**.

---

# 🚀 Example: Create a Simple Project

```powershell
cd Desktop

mkdir myproject

cd myproject

New-Item server.js
New-Item .env
New-Item package.json

code .
```

Your project will look like:

```text
myproject/
├── server.js
├── .env
└── package.json
```

---

# 📌 Quick Command Reference

| Task                      | Command                                                 |
| ------------------------- | ------------------------------------------------------- |
| Show current folder       | `pwd`                                                   |
| List files                | `ls`                                                    |
| Enter folder              | `cd folder`                                             |
| Go back                   | `cd ..`                                                 |
| Create file               | `New-Item file.txt`                                     |
| Create folder             | `mkdir folder`                                          |
| Copy files                | `Copy-Item "source\*" "destination\" -Recurse`          |
| Copy folder               | `Copy-Item "source" "destination" -Recurse`             |
| Copy/replace file content | `Get-Content source.txt \| Set-Content destination.txt` |
| Append file content       | `Get-Content source.txt \| Add-Content destination.txt` |
| Delete file               | `Remove-Item file.txt`                                  |
| Delete folder             | `Remove-Item folder -Recurse`                           |
| Force delete              | `Remove-Item folder -Recurse -Force`                    |
| Open VS Code              | `code .`                                                |

---

## ⚠️ Important

Be especially careful with:

```powershell
Remove-Item "folder" -Recurse -Force
```

It can delete a folder and its contents permanently.
