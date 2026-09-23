If you want to copy all files from one folder to another
Copy-Item "C:\Users\Anurag\Desktop\project1" "C:\Users\Anurag\Desktop\project2" -Recurse
Copy-Item "C:\source\*" "C:\destination\" -Recurse

If you want to copy the entire folder
Copy-Item "C:\Users\Anurag\Desktop\project1" "C:\Users\Anurag\Desktop\project2" -Recurse


If you mean copy all content from one file into another existing file
Get-Content "source.txt" | Set-Content "destination.txt"

If you want to append instead:
Get-Content "source.txt" | Add-Content "destination.txt"