# Day 06 – Linux Fundamentals: Read and Write Text Files 

## Creating a file 
- touch notes.txt (creates empty file )

## Writing tect to file 
- echo "content" > notes.txt (> means overwrite , if something is there it will get erase )
- echo "content2" >> notes.txt (>> means redirects without deleting anything)
- echo "content3" | tee -a notes.txt (tee -a use to see output and save it )

## REading the file back 
- cat notes.txt (used to read file from top to end ) #avoid when file is large
- head -n 2 notes.txt (display -n lines from top , default 10)
- tail -n 2 notes.txt (dispaly -n lines from bottom )

<img width="1348" height="1352" alt="image" src="https://github.com/user-attachments/assets/2aebcff2-4511-4318-a713-1ee6e87a04a4" />

## Real world example 
- tail -f /var/log/syslog (tail -f is used to view file in real time , best to check log in real time )

<img width="2756" height="604" alt="image" src="https://github.com/user-attachments/assets/b655876b-6762-4613-9dcc-9f37f1fcfa25" />
